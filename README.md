# SCAD Parametric Editor

Local web UI for editing a parametric OpenSCAD template, rendering a preview, and exporting STL/3MF.

## What this does
- Edit `parametric_clamp.scad` in a browser form
- Save changes back to disk
- Render a PNG preview (OpenSCAD)
- Export STL or 3MF (OpenSCAD)

## Files and paths (current setup)
- Web app: `/Users/kevinwolf/scad_form/app.py`
- SCAD being edited: `/Users/kevinwolf/Downloads/parametric_clamp.scad`
- Exports: `/Users/kevinwolf/Downloads/exports/parametric.stl` and `/Users/kevinwolf/Downloads/exports/parametric.3mf`
- Preview image: `/Users/kevinwolf/Downloads/exports/parametric_preview.png`

## Requirements
- Python 3
- OpenSCAD (CLI binary)
- BOSL2 library

## One-time setup (macOS)
1) Install OpenSCAD (Homebrew cask):

```sh
brew install --cask openscad
```

2) Approve OpenSCAD in macOS Gatekeeper (first run)
- System Settings → Privacy & Security → “Open Anyway” for OpenSCAD

3) Install BOSL2 (OpenSCAD library)

```sh
mkdir -p ~/Documents/OpenSCAD/libraries

git clone https://github.com/BelfrySCAD/BOSL2.git \
  ~/Documents/OpenSCAD/libraries/BOSL2
```

## Run the editor

```sh
/opt/homebrew/bin/python3 /Users/kevinwolf/scad_form/app.py
```

Open in browser:

```
http://127.0.0.1:8000
```

## Usage
1) Edit fields in the form
2) Click **Save SCAD**
3) Click **Render Preview** to generate a PNG preview
4) Click **Export STL** or **Export 3MF**

## Clamp (vise) option
The SCAD includes an optional side clamp block + through-hole.
Form fields:
- `clamp_enabled` (bool)
- `clamp_side` (`left` or `right`)
- `clamp_overhang` (mm)
- `clamp_block_width` (mm, along Y)
- `clamp_hole_d` (mm)

Defaults in `parametric_clamp.scad`:
- `clamp_enabled = true`
- `clamp_side = "left"`
- `clamp_overhang = 25`
- `clamp_block_width = 25`
- `clamp_hole_d = 8.5` (M8 clearance)

## Preview notes
Preview uses OpenSCAD to render a PNG. It can take a few seconds depending on settings.

## Troubleshooting
- **Export fails:** Ensure OpenSCAD is installed and approved by Gatekeeper.
- **Missing BOSL2:** Install BOSL2 into `~/Documents/OpenSCAD/libraries/BOSL2`.
- **Preview not showing:** Click Render Preview again; the app serves `/preview.png`.

## Customize paths
Update these constants in `app.py`:
- `SCAD_PATH`
- `EXPORT_DIR`
- `OPENSCAD_CANDIDATES`
