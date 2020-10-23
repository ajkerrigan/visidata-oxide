# visidata-oxide

![PyOxidizer Build](https://github.com/ajkerrigan/visidata-oxide/workflows/PyOxidizer%20Build/badge.svg)

Experiments using [PyOxidizer](https://pyoxidizer.readthedocs.io/) to build [VisiData](https://www.visidata.org/) binaries that bring their own embedded Python.

### Building

* [Install PyOxidizer](https://pyoxidizer.readthedocs.io/en/stable/getting_started.html#installing)
* Clone this repository locally
* Change to the repository directory and run:

```
pyoxidizer run
```

A successful build will produce a `visidata-oxide` binary inside `/path/to/visidata-oxide/build/<platform>/debug/install`. Alongside that binary there will be a `lib` directory containing Python dependencies.

### Usage

Test the build by running:

```
/path/to/visidata-oxide/build/<platform>/debug/install/visidata-oxide
```

If you get a VisiData menu and no angry errors, that's success!

To make it somewhat more friendly, you can move or link the contents of the `install` directory (both the `visidata-oxide` binary and `lib` directory) to a location on your system path. Then you should be able to run `visidata-oxide` as needed.

### Adding Python Dependencies

This package builds a fairly "batteries included" flavor of VisiData that includes Python dependencies behind a number of VisiData plugins and loaders.

The `visidata-oxide` binary includes an embedded Python runtime but no pip, so VisiData's native plugin functionality won't function normally. If you have a working Python 3.8 environment, you can use pip with the `--target` switch to have it operate against the visidata-oxide `lib` directory.

If you _don't_ have a working Python 3.8 environment, you can still download Python package files from PyPI and copy them into the visidata-oxide `lib` directory manually.

### Why?!

Why not?

VisiData provides installation instructions for a variety of package managers and platforms. However, the experiments here _could_ lead to a download/extract/run option that might be useful in some environments.

### Known Issues

* Due to some included dependencies, we tell PyOxidizer to [package files instead of in-memory resources](https://pyoxidizer.readthedocs.io/en/stable/packaging_additional_files.html). That means we don't get a single self-contained binary, but it also means that the build works 😁.

* Trying to install plugins from the VisiData plugins bazaar (`open-plugins`) will not work. You _can_ still add Python dependencies as described above and manually install plugins to `~/.visidata/plugins`.
