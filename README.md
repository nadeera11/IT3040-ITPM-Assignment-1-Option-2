# PixelsSuite Preview – Playwright Automation

Automated UI test that verifies the **image preview functionality** on
[https://www.pixelssuite.com/](https://www.pixelssuite.com/) by uploading a PNG
file to the *Convert to PNG* tool and checking that the website renders the
preview. The result is appended as a row to `execution_results.csv` and a
full-page screenshot is saved under `results/`.

This project is the automated component of **IT3040 Assignment 1 – Option 2**.

## Project structure

```
test_automation_ui/
├── image_preview_test.py      # Playwright test script
├── sample.png                 # PNG fixture uploaded by the test
├── execution_results.csv      # Test result log (header + one row per run)
├── results/
│   └── preview_pass.png       # Screenshot produced by the latest run
└── README.md
```

## Prerequisites

- Python **3.11** or **3.12** (3.14 also works)
- Google Chrome (recommended) — or let Playwright install Chromium automatically
- Windows, macOS, or Linux

Verify Python is installed:

```
python --version
```

## Installation

From the project root (e.g. `D:\test_automation_ui`):

```
pip install -U pip
pip install playwright openpyxl
playwright install
```

The last command downloads the Chromium browser used by Playwright (~110 MB).

## Running the test

From the project root:

```
python image_preview_test.py --url "https://www.pixelssuite.com/convert-to-png" --slow-mo-ms 2000
```

The script will:

1. Launch Chromium and open the target URL.
2. Locate the file-upload input and upload `sample.png`.
3. Wait for a preview element (`img` / `canvas` / `svg` / `video`) to appear next
   to a "Preview" label.
4. Take a full-page screenshot to `results/preview_<status>.png`.
5. Append a row to `execution_results.csv`.

### Command-line options

| Flag | Default | Description |
|------|---------|-------------|
| `--url` | `https://www.pixelssuite.com/convert-to-png` | Page under test |
| `--png` | `sample.png` | PNG file to upload (auto-created if missing) |
| `--out-dir` | `results` | Folder where screenshots are written |
| `--csv` | `execution_results.csv` | Output CSV path |
| `--headless` | off | Run browser without a visible window |
| `--timeout-ms` | `60000` | Per-step timeout in milliseconds |
| `--slow-mo-ms` | `0` | Delay between Playwright actions (ms) — useful for demos |

## Expected output

Console (truncated):

```
========== TEST RESULT ==========
PNG file        : <abs path>\sample.png
Preview detected: True
Status          : PASS
Screenshot      : <abs path>\results\preview_pass.png
CSV             : <abs path>\execution_results.csv
```

`execution_results.csv` after a successful run:

| file_type | file_path | preview_detected | status | screenshot |
|-----------|-----------|------------------|--------|------------|
| PNG | …\sample.png | True | PASS | …\results\preview_pass.png |

## Troubleshooting

- **`File upload input was not found`** — the page layout changed or did not
  finish loading. Re-run with `--timeout-ms 90000`.
- **`playwright` not found** — run `pip install playwright` and
  `playwright install` again.
- **Browser does not launch on Windows** — make sure no antivirus is blocking
  the Chromium binary under `%LOCALAPPDATA%\ms-playwright\`.

## Assignment context

This automation covers one of the 36 test scenarios required by IT3040
Assignment 1 – Option 2 (preview functionality of the *Convert to PNG* feature).
The remaining 35 manual test scenarios are documented in
`Manual Test Cases for Option 2.xlsx`.

## Author

- **Registration number:** IT23861268
- **Email:** it23861268@my.sliit.lk
- **Module:** IT3040 – ITPM, Semester 1
- **Assignment:** Assignment 1 – Option 2 (Functional and Usability Testing)
