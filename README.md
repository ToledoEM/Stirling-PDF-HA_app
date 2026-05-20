# Stirling-PDF Home Assistant Add-on Repository

A Home Assistant OS add-on repository that packages [Stirling-PDF](https://github.com/Stirling-Tools/Stirling-PDF) — a locally hosted, feature-rich PDF manipulation tool — in three variants to suit different needs.

## Add-ons

### Stirling-PDF Ultra-Lite

Minimal install. Core PDF operations only with the smallest possible image. **Requires 1 GB RAM minimum.**

**Included:** merge, split, rotate, convert, password protection.

**Not included:** OCR, LibreOffice conversion, Ghostscript, ImageMagick, pipeline automation.

→ [Documentation](stirling_pdf_ultra_lite/README.md)

---

### Stirling-PDF Full

All features pre-configured and ready to use. **Requires 2 GB RAM minimum.**

**Included:** merge, split, compress, rotate, watermark, sign, annotate, redact, OCR (Tesseract), image↔PDF conversion, pipeline automation, REST API.

→ [Documentation](stirling_pdf_full/README.md)

---

### Stirling-PDF Fat

Full features plus additional fonts and pre-bundled jar security. Uses the `latest-fat` upstream image. **Requires 4 GB RAM minimum.**

**Adds over Full:** extra fonts, PDF↔Word/PowerPoint/RTF (LibreOffice), Ghostscript, ImageMagick, Weasyprint, PDF→HTML/Markdown.

→ [Documentation](stirling_pdf_fat/README.md)

---

## Which one should I install?

| I want to… | Use |
|---|---|
| Basic merge, split, rotate, password | Ultra-Lite |
| OCR, image conversion, pipelines | Full |
| Convert Word/PowerPoint/RTF to PDF | Fat |
| Minimal storage / slow connection | Ultra-Lite |
| Every possible feature | Fat |

All three can be installed simultaneously — they use different slugs and separate storage paths.

## Installation

1. In Home Assistant, go to **Settings → Add-ons → Add-on Store**.
2. Click the menu (⋮) in the top right and select **Repositories**.
3. Add this repository URL and click **Add**.
4. Find **Stirling-PDF Ultra-Lite**, **Stirling-PDF Full**, or **Stirling-PDF Fat** in the store and click **Install**.
