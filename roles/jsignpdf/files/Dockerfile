# Dockerfile for jsignpdf
#
# Usage:
# Build the image
# docker build -t jsignpdf:latest /usr/local/share/jsignpdf/
# # Start the jsignpdf
# docker run -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY -v $HOME/credentials:/app/credentials:ro -v /tmp/workdir:/app/workdir --rm jsignpdf:latest
#
FROM debian:latest
ARG JSIGN_VERSION=2.1.0
ENV JSIGN_SHA512 24443b6383696686fa75cba65874f76382269131d2bb7599fb4ee722496bbf67c1b015fb1dc191209a12de5c85e4d9ca6324c70817287ef096c72d2907d625c1
RUN apt-get update \
    && apt-get install --yes --no-install-recommends \
        curl \
        default-jre \
        unzip

WORKDIR /app

RUN curl -L --output jsignpdf.zip "https://sourceforge.net/projects/jsignpdf/files/stable/JSignPdf%20${JSIGN_VERSION}/jsignpdf-${JSIGN_VERSION}.zip/download?use_mirror=netix" \
    && echo "$JSIGN_SHA512 *jsignpdf.zip" | sha512sum -c - \
    && unzip jsignpdf.zip \
    && rm jsignpdf.zip \
    && chown -R 1000:1000 .

USER 1000:1000

ENV JSIGN_VERSION=${JSIGN_VERSION}
CMD ["sh", "-c", "java -jar jsignpdf-${JSIGN_VERSION}/JSignPdf.jar"]
