# MarekOnd's homepage

## Compilation

### Cloning repo

```bash
git clone https://github.com/MarekOnd/MarekOnd.github.io.git

git submodule update --init --recursive
```

#### How to correct submodule versions

```bash
git submodule update --remote --merge
```

### Local server

Basic server

```bash
hugo server
```

compile everything on update - `--disableFastRender`
with unpublished stuff - `--buildDrafts`