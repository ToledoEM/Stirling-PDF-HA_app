# Stirling-PDF — Home Assistant Add-on

[Stirling-PDF](https://github.com/Stirling-Tools/Stirling-PDF) is a locally hosted web application for performing operations on PDF files. This add-on packages the official `stirlingtools/stirling-pdf` Docker image and exposes the web UI through Home Assistant.

## Features

- **60+ PDF tools** — merge, split, compress, convert, sign, edit, watermark, and more
- **Stateful processing** — upload once, use across multiple tools without re-uploading
- **Undo & redo** — full version history
- **OCR support** — Tesseract-based text recognition with multi-language support (38+ languages)
- **Pipeline automation** — watched-folder batch processing
- **Local processing** — files never leave your network; deleted automatically after each task
- **Optional authentication** — built-in login system for multi-user environments
- **API access** — REST API for automation and integrations

## Installation

1. Go to **Settings → Add-ons → Add-on Store** in Home Assistant.
2. Add this repository via the menu (⋮) → **Repositories**.
3. Find **Stirling-PDF** and click **Install**.
4. Start the add-on and open the Web UI.

## Configuration

| Option | Default | Description |
|---|---|---|
| `enable_login` | `false` | Enable Stirling-PDF's built-in authentication. Set to `true` for multi-user environments. |
| `langs` | `en_GB` | Comma-separated Tesseract OCR language codes, e.g. `en_GB,fra,deu`. |
| `log_level` | `info` | Log verbosity: `info`, `debug`, `warn`, or `error`. |

### Example configuration

```yaml
enable_login: false
langs: en_GB
log_level: info
```

To enable login and add Spanish OCR support:

```yaml
enable_login: true
langs: en_GB,spa
log_level: warn
```

## Persistent Storage

Data is stored on your Home Assistant host so it survives add-on updates and restarts.

| Data | Host path |
|---|---|
| Configuration & database (`settings.yml`) | `/config/stirling_pdf/configs/` |
| Application logs | `/config/stirling_pdf/logs/` |
| Tesseract OCR language files | `/share/stirling_pdf/tessdata/` |
| Pipeline / watched folders | `/share/stirling_pdf/pipeline/` |

### Adding OCR languages

Download `.traineddata` files from the [Tesseract tessdata repository](https://github.com/tesseract-ocr/tessdata) and place them in `/share/stirling_pdf/tessdata/` on your host. Then add the language code to the `langs` option and restart the add-on.

### Pipeline automation

Place PDF files in `/share/stirling_pdf/pipeline/watchedFolders/` to trigger automated processing. Completed outputs appear in `/share/stirling_pdf/pipeline/finishedFolders/`.

## Accessing the UI

After the add-on starts, click **Open Web UI** in the add-on panel, or navigate to `http://homeassistant.local:8080`.

## Architecture Notes

This add-on uses a two-stage Docker build:

1. The Stirling-PDF application is copied from the official `stirlingtools/stirling-pdf:latest` image.
2. It is embedded into the Home Assistant base image, which provides s6-overlay process supervision and the `bashio` scripting library.

Only `amd64` and `aarch64` architectures are supported. The Stirling-PDF JVM does not run on `armhf`, `armv7`, or `i386`.

## Changelog

### 0.36.9
- Initial release.

## Support

- Stirling-PDF documentation: [docs.stirlingpdf.com](https://docs.stirlingpdf.com)
- Stirling-PDF issues: [github.com/Stirling-Tools/Stirling-PDF](https://github.com/Stirling-Tools/Stirling-PDF)
- Add-on issues: open an issue in this repository
