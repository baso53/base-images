FROM arm32v6/node:iron-alpine as dev

WORKDIR /usr/src/app

ENV LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH \
    LD_RUN_PATH=/usr/local/lib:$LD_RUN_PATH

# Update and install dependencies with apk
RUN apk update && \
    apk add --no-cache \
        autoconf \
        build-base \
        jq \
        perl \
        perl-net-ssleay \
        perl-io-socket-ssl \
        perl-capture-tiny \
        perl-file-which \
        perl-file-chdir \
        perl-ffi-checklib \
        perl-test-warnings \
        perl-test-fatal \
        perl-test-needs \
        perl-test2-suite \
        perl-path-tiny \
        perl-try-tiny \
        perl-term-table \
        perl-mojolicious \
        perl-file-slurper \
        libexif-dev \
        expat-dev \
        glib-dev \
        libgsf-dev \
        libheif-dev \
        libjpeg-turbo-dev \
        libjxl-dev \
        lcms2-dev \
        orc-dev \
        librsvg-dev \
        libspng-dev \
        libwebp-dev \
        meson \
        ninja-build \
        pkgconf \
        wget \
        zlib-dev \
        perl-app-cpanminus \
        jq \
        bash \
        ffmpeg
        # ffmpeg-libavcodec \
        # ffmpeg-libavformat \
        # ffmpeg-libavutil \
        # ffmpeg-libavfilter \
        # ffmpeg4-libavdevice \
        # ffmpeg4-libswresample \
        # ffmpeg-libswscale


COPY bin/* ./
RUN ./build-libraw.sh
RUN ./build-imagemagick.sh
RUN ./build-libvips.sh
RUN ./build-perllib-compress-brotli.sh

ADD https://download.geonames.org/export/dump/cities500.zip /usr/src/resources/cities500.zip
ADD --chmod=444 https://download.geonames.org/export/dump/admin1CodesASCII.txt /usr/src/resources/admin1CodesASCII.txt
ADD --chmod=444 https://download.geonames.org/export/dump/admin2Codes.txt /usr/src/resources/admin2Codes.txt

RUN umask 0333 && unzip /usr/src/resources/cities500.zip -d /usr/src/resources/ && \
    rm /usr/src/resources/cities500.zip && date --iso-8601=seconds | tr -d "\n" > /usr/src/resources/geodata-date.txt
