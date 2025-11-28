# Installation

If you are unfamiliar with python or the command line, instead use the bundled app installer as demonstrated in [Beginner Setup](beginner_setup.md).

## Install with uv (Recommended)

[uv](https://docs.astral.sh/uv/) is the newest and fastest way to manage Python libraries. It's easy to install and simplifies environment management. [Install uv here](https://docs.astral.sh/uv/getting-started/installation/).

Recommended: Install napari-ndev as a uv tool, with optional dependencies including sample data, themes, and additional plugins:

```bash
uv tool install napari-ndev[all]
```

Then launch napari with the nDev App widget open:

```bash
napari -w napari-ndev "nDev App"
```

This is equivalent to `napari -w napari-ndev "nDev App"`. Additional plugins installed via napari's plugin menu persist between sessions.

To update:

```bash
uv tool upgrade napari-ndev
```

Alternatively, create a dedicated virtual environment:

```bash
uv venv
# On Windows:
.venv\Scripts\activate
# On macOS/Linux:
source .venv/bin/activate

uv pip install napari-ndev[all]
```

## Install with pip

**napari-ndev** is a pure Python package and can be installed with [pip] (recommended in a [managed environment](https://biapol.github.io/blog/mara_lampert/getting_started_with_mambaforge_and_python/readme.html)):

```bash
pip install napari-ndev[qtpy-backend]
```

This installs napari-ndev with napari and PyQt6 (the Qt backend).

The easiest way to get started is to install all optional dependencies:

```bash
pip install napari-ndev[all]
```

After installation, launch napari with the nDev App widget open:

```bash
napari-ndev
```

### Optional Dependencies

**napari-ndev** provides several optional dependency groups:

- **`[qtpy-backend]`** - Includes `napari[pyqt6]` for the Qt GUI
- **`[extras]`** - Additional napari plugins (napari-assistant, simpleitk-image-processing, segment-blobs-and-things-with-membranes)
- **`[all]`** - Everything above plus ndev-sampledata and ndev-themes (recommended for most users)

Install specific groups as needed:

```bash
pip install napari-ndev[extras]  # Just additional plugins
```

### Additional Image Format Support

**napari-ndev** uses [ndevio](https://github.com/ndev-kit/ndevio) for image I/O, which relies on [bioio](https://github.com/bioio-devs/bioio) readers. Basic formats (TIFF, OME-TIFF, OME-Zarr, PNG, JPEG) work out of the box.

For additional proprietary formats, install the appropriate bioio reader:

```bash
# CZI files (GPL-3 licensed)
pip install bioio-czi

# LIF files (GPL-3 licensed)
pip install bioio-lif

# Bio-Formats for many formats (functionality not guaranteed)
pip install bioio-bioformats
```

**License Note:** Some bioio readers (like bioio-czi and bioio-lif) are GPL-3 licensed. If you install and use these, you must comply with GPL-3 license terms. See the [bioio documentation](https://bioio-devs.github.io/bioio/) for the full list of available readers.

## Install with Pixi (For Development)

[Pixi](https://pixi.sh) provides reproducible, cross-platform environments and is excellent for development.

Clone the repository and use Pixi:

```bash
git clone https://github.com/ndev-kit/napari-ndev.git
cd napari-ndev
```

Launch napari with the nDev App:

```bash
pixi run napari-ndev
```

Or install in editable mode and activate the environment:

```bash
pixi install              # Default environment with qtpy-backend
pixi install -e dev       # Development environment with testing tools

pixi shell                # Activate the environment
napari                    # Run napari or any command
```

Run tests:

```bash
pixi run -e dev test
```

The `pixi.toml` defines several environments:

- `default` - Minimal installation with qtpy-backend
- `all` - All optional dependencies
- `extras` - Additional napari plugins only
- `dev` - Development environment with testing tools (pytest, ruff, pre-commit)

### Development with uv

For development with uv, clone the repository and create a virtual environment:

```bash
git clone https://github.com/ndev-kit/napari-ndev.git
cd napari-ndev

uv venv -p 3.13
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

uv pip install -e . --group dev
```

Run tests:

```bash
uv run pytest -v
```
