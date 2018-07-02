# docker-planetaryimager
#

## Builder
#

FROM debian:stretch-slim as builder

### default ARG(s)
#
ARG planetaryImager__tag=v0.7.0
ARG planetaryImager__git=https://github.com/GuLinux/PlanetaryImager

### default Workdir
#
WORKDIR /opt

### Build dependancies
#
RUN set -xe; \
    \
    buildDeps=' \
        build-essential \
        ca-certificates \
        cmake \
        git \
        libopencv-dev \
        libboost-all-dev \
        libcfitsio-dev \
        libusb-1.0-0-dev \
        libccfits-dev \
        qtbase5-dev \
        qtdeclarative5-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    '; \
    apt-get update; \
    apt-get install -y --no-install-recommends $buildDeps; \
    rm -rf /var/lib/apt/lists/*;
    
### Clone Planetary Imager sources
#
RUN set -xe; \
    \
    git clone --recursive -b $planetaryImager__tag $planetaryImager__git

### Build Planetary Imager .tar.gz package
#
RUN set -xe; \
    \
    cd PlanetaryImager; \
    mkdir build; \
    cd build; \
    cmake .. -DCMAKE_INSTALL_PREFIX=/usr; \
    make package

## Runtime
#

FROM debian:stretch-slim

### default Workdir
#
WORKDIR /opt

### Install run dependancies
#
RUN set -xe; \
    \
    deps=' \
        fxload \
        libopencv-contrib2.4v5 \
        libopencv-core2.4v5 \
        libopencv-highgui2.4-deb0 \
        libopencv-imgproc2.4v5 \
        libopencv-ts2.4v5 \
        libopencv-stitching2.4v5 \
        libopencv-superres2.4v5 \
        libopencv-videostab2.4v5 \
        libusb-1.0-0 \
        libccfits0v5 \
        libqt5gui5 \
        libqt5opengl5 \
        libqt5qml5 \
        libqt5network5 \
        libqt5widgets5 \
    '; \
    apt-get update; \
    apt-get install -y --no-install-recommends $deps; \
    rm -rf /var/lib/apt/lists/*;

### Get Planetary Imager .tar.gz Package from Builder stage
#
COPY --from=builder /opt/PlanetaryImager/build/*.tar.gz .

### Extract .tar.gz Package
#
RUN set -xe; \
    \
    tar xf *.tar.gz --strip-components=1 -C /

CMD ["planetary_imager"]