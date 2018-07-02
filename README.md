# [![Planetary Imager Logo][planetaryimager-logo]](https://blog.gulinux.net/en/planetary-imager) docker-planetaryimager

*Qt capture software for astronomy, mainly planetary shooting.*

[![RSS commits][rss-commits]](https://github.com/src386/docker-planetaryimager/commits/master.atom)

[planetaryimager-logo]: https://raw.githubusercontent.com/src386/docker-planetaryimager/master/lib/images/planetary_imager_small.png
[rss-commits]: https://img.shields.io/badge/RSS-commits-orange.svg

[Planetary Imager][planetaryimager] is a fast, simple to use software for solar system imaging. Currently supports V4L2, ZWO and QHY devices.

[planetaryimager]: https://blog.gulinux.net/en/planetary-imager

## Supported tags and respective `Dockerfile` links

- [`0.7.0`][dockerfile-0.7.0], [`latest`][dockerfile-latest] ([0.7.0/Dockerfile][dockerfile-latest])

[dockerfile-latest]: https://github.com/src386/docker-planetaryimager/blob/master/0.7.0/Dockerfile
[dockerfile-5.6]: https://github.com/src386/docker-planetaryimager/blob/master/0.7.0/Dockerfile

## Quick start


```
docker run \
  --volume=/tmp/.X11-unix:/tmp/.X11-unix \
  --device=/dev/dri:/dev/dri \
  --env="DISPLAY" \
  --privileged planetary-imager:dev
```

Or, using docker-compose (recommended):

```
version: '3'
services:

  planetaryimager:
    image: src386/docker-planetaryimager:latest
    devices:
      - /dev/dri:/dev/dri
    environment:
      - DISPLAY
    volumes:
      - /tmp/.X11-unix:/tmp/.X11-unix
    privileged: true
```

Then fire up a Planetary Imager container:

    docker-compose up -d

Features
--------

- Image currently based on debian:stretch-slim

Development
-----------

For example if you want to build the 0.7.0 image:

    git clone https://github.com/src386/docker-planetaryimager
    cd docker-planetaryimager/0.7.0 && docker build -t docker-planetaryimager:0.7.0 .

Or you may want to use the docker-compose.yml file:

    cd docker-planetaryimager/0.7.0 && docker-compose build

## FAQ

### How do I delete install.php ?

Restart the container. If install.php is still present, open an issue.

## Licensing

Since Planetary Imager is under [GNU General Public License][gnugpl], docker-planetaryimager too.
You can find full text of the license in the [LICENSE][license] file.

[gnugpl]: http://www.gnu.org/licenses/gpl.html
[license]: https://github.com/src386/docker-planetaryimager/blob/master/LICENSE
