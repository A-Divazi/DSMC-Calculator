# Building DSMC-Calculator

The app is a single-file Tkinter program (`dsmc_calc.py`), so no compilation is
needed to run it. The prebuilt executables are created with **PyInstaller**.
`DSMC_Calculator.spec` in the repository root holds the PyInstaller
configuration used to build them.

## Build requirements

- Python 3 with **Tkinter**.
- [PyInstaller](https://pyinstaller.org): `pip install pyinstaller`.

## Build a standalone executable

From the repository root:

```bash
pyinstaller DSMC_Calculator.spec
```

This produces a single-file, windowed (no console) executable:

- **Linux** → `dist/DSMC_Calculator_Linux`
- **Windows** → `dist/DSMC_Calculator.exe`

> The `.spec` sets `console=False`, so no terminal window is shown — the app
> launches directly as a GUI. If you need a console for debugging during
> development, change `console=True` in the spec and rebuild.

### Rebuilding for each platform

PyInstaller is **not** cross-compiling: build the Linux binary **on Linux** and
the Windows binary **on Windows**. Build each platform's executable on that
platform and place the result in `releases/` (the current names are
`DSMC_Calculator_Linux` and `DSMC_Calculator_Windows.exe`).

### Manual one-file build (alternative)

```bash
pyinstaller --onefile --windowed --name DSMC_Calculator dsmc_calc.py
```

## Notes

- The spec file pins the settings that produced the shipped executables. If you
  change `dsmc_calc.py`, rebuild and re-upload the executables in `releases/`.
- Keep only the finished executables in `releases/`; the intermediate
  `build/` and `dist/` folders are git-ignored (see `.gitignore`).
