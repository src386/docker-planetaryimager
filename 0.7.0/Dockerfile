# Builder
#

FROM debian:stretch-slim as builder

WORKDIR /opt

RUN apt-get update && apt-get install -y --no-install-recommends \
    \
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
    libpng-dev

RUN git clone --recursive -b v0.7.0 https://github.com/GuLinux/PlanetaryImager.git

RUN cd PlanetaryImager && mkdir build && cd build; \
    cmake .. -DCMAKE_INSTALL_PREFIX=/usr && make package

# Runtime
#

FROM debian:stretch-slim

WORKDIR /opt

RUN apt-get update && apt-get install -y --no-install-recommends \
    \
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
        libqt5widgets5

COPY --from=builder /opt/PlanetaryImager/build/PlanetaryImager-0.7.0-Linux-x86_64.tar.gz .

RUN tar xf /opt/PlanetaryImager-0.7.0-Linux-x86_64.tar.gz --strip-components=1 -C /