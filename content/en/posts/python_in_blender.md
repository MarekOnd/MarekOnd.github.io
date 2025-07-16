---
title: "Python in Blender with packages"
date: 2025-07-16T08:08:06+02:00
draft: true
---

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
