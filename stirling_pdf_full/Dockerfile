ARG BUILD_FROM=ghcr.io/home-assistant/amd64-base:3.23
# hadolint ignore=DL3007
FROM stirlingtools/stirling-pdf:latest-fat AS stirling

FROM ${BUILD_FROM}

# hadolint ignore=DL3018
RUN apk add --no-cache \
      bash \
      coreutils \
      jq \
      openssl \
      ca-certificates \
      openjdk21-jre-headless

# Copy the Stirling-PDF application and its runtime assets from upstream fat image
COPY --from=stirling /app /app
COPY --from=stirling /scripts /scripts
COPY --from=stirling /configs /configs
COPY --from=stirling /logs /logs
COPY --from=stirling /pipeline /pipeline
COPY --from=stirling /customFiles /customFiles
COPY --from=stirling /usr/share/tesseract-ocr /usr/share/tesseract-ocr
COPY --from=stirling /usr/lib/libreoffice /usr/lib/libreoffice
COPY --from=stirling /usr/bin/soffice /usr/bin/soffice
COPY --from=stirling /opt/venv /opt/venv
COPY --from=stirling /usr/bin/gs /usr/bin/gs
COPY --from=stirling /usr/bin/qpdf /usr/bin/qpdf
COPY --from=stirling /usr/bin/magick /usr/bin/magick
COPY --from=stirling /usr/bin/tesseract /usr/bin/tesseract
COPY --from=stirling /usr/bin/pdftohtml /usr/bin/pdftohtml

COPY run.sh /run.sh
COPY rootfs /

RUN chmod +x /run.sh \
    && chmod +x /etc/s6-overlay/s6-rc.d/stirling_pdf_full/run \
    && chmod +x /etc/s6-overlay/s6-rc.d/stirling_pdf_full/finish

ARG BUILD_VERSION
LABEL \
  io.hass.version="${BUILD_VERSION}" \
  io.hass.type="addon" \
  io.hass.arch="aarch64|amd64"

ENTRYPOINT ["/init"]
