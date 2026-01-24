---
title: "Python in Blender with packages"
date: 2025-07-16T08:08:06+02:00
draft: false
cover:
    image: "brno-osmnx-render.png"
    alt: "Render of the road network of Brno"
    caption: "Render of the road network of Brno"
    relative: false
---



Below is a method to install python packages to Blender with access to file directory so that 
the packages can perform more complex tasks. Using this method `osmnx` python package was able to 
download map data of the road network of a city and create mesh out of them.

## Install Blender from flatpak

```bash
flatpak install org.blender.Blender
```

## Initialize pip

```bash
flatpak run --command=python3 org.blender.Blender -m ensurepip
```

## Install packages

- open Blender
- go to `Scripting`
- create a script called `install_packages` (the name can be arbitrary) with the following contents:

```python
import subprocess
import sys
subprocess.check_call([sys.executable, "-m", "pip", "install", "--user", "[INSERT PACKAGES TO INSTALL]"])
```

- run the script

{{<tip>}}
Any errors during installation will be shown in the lower left corner in Blender UI.
{{</tip>}}

{{<warning>}}
The environment of Python inside Blender is read-only. We are creating another directory with the `--user` argument so that packages can cache necessary data (needed e.g. for [osmnx](https://github.com/gboeing/osmnx)).
{{</warning>}}

## Connect user packages to Blender

- create another script called `initialize` (the name can be arbitrary) with the following contents:

```python
import site
site.addsitedir(site.USER_SITE)
```

- run the script

{{<tip>}}
This needs to rerun in each session in Blender to have the directory with packages included. The packages need to be installed only once.
{{</tip>}}

## Include and use packages in Python scripts in Blender

```python
import osmnx as ox

[...]
```

## Example: Get road network map of a city and visualize

{{<tip>}}
This process can take a long time and there is no feedback until everything finishes. (Blender can also sometimes completely freeze)
{{</tip>}}

```python
import os
import osmnx as ox
import shapely
import bpy

# Setup
os.chdir(os.path.expanduser("~"))
ox.settings.cache_folder = os.path.expanduser("~/.cache/osmnx")
ox.settings.use_cache = True
ox.settings.log_console = True

# Get road network
G = ox.graph.graph_from_place("Berlin, Germany", network_type="drive",simplify=False)
edges = ox.convert.graph_to_gdfs(G, nodes=False, edges=True)

# Deduplicate vertices
vert_map = {}  # (x, y) -> index
all_verts = []
all_edges = []

for row in edges.itertuples():
    geom = row.geometry
    if not isinstance(geom, shapely.geometry.LineString):
        continue

    coords = [(x, y) for x, y in geom.coords]  # round to avoid float noise
    if len(coords) < 2:
        continue

    edge_idx = []
    for pt in coords:
        if pt not in vert_map:
            vert_map[pt] = len(all_verts)
            all_verts.append((pt[0], pt[1], 0))
        edge_idx.append(vert_map[pt])

    all_edges.extend([(edge_idx[i], edge_idx[i+1]) for i in range(len(edge_idx)-1)])

# Create one single mesh and object
mesh = bpy.data.meshes.new("OSM_Roads")
mesh.from_pydata(all_verts, all_edges, [])
mesh.update()

obj = bpy.data.objects.new("OSM_Roads", mesh)
bpy.context.collection.objects.link(obj)
```
