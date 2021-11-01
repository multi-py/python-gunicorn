# python-gunicorn

A multiarchitecture container image for running Python with Gunicorn.

Looking for the containers? [Head over to the Github Container Registry](https://github.com/multi-py/python-gunicorn/pkgs/container/python-gunicorn)!

## Benefits

### Multi Architecture Builds

Every tag in this repository supports these architectures:

* linux/amd64
* linux/arm64
* linux/arm/v7


### Small Images via Multi Stage Builds

All libraries are compiled in one image before being moved into the final published image. This keeps all of the build tools out of the published container layers.

### No Rate Limits

This project uses the Github Container Registry to store images, which have no rate limiting on pulls (unlike Docker Hub).

### Rapid Building of New Versions

Within 30 minutes of a new release to gunicorn on PyPI builds will kick off for new containers. This means new versions can be used in hours, not days.

### Regular Updates

Containers are rebuilt weekly in order to take on the security patches from upstream containers.

## How To

### Full
To pull the latest slim version:

```bash
docker pull ghcr.io/multi-py/python-gunicorn:py3.10-LATEST
```

To include it in the dockerfile instead:

```dockerfile
FROM ghcr.io/multi-py/python-gunicorn:py3.10-LATEST
```

### Slim

To pull the latest slim version:

```bash
docker pull ghcr.io/multi-py/python-gunicorn:py3.10-slim-LATEST
```

To include it in the dockerfile instead:

```dockerfile
FROM ghcr.io/multi-py/python-gunicorn:py3.10-slim-LATEST
```

### Copy Just the Packages
It's also possible to copy just the Python packages themselves. This is particularly useful when you want to use the precompiled libraries from multiple containers.

```dockerfile
FROM python:3.10

COPY --from=ghcr.io/multi-py/python-gunicorn:py3.10-slim-LATEST /usr/local/lib/python3.10/site-packages/* /usr/local/lib/python3.10/site-packages/
```

### Add Your App

By default the startup script checks for the following packages and uses the first one it can find-

* `/app/app/main.py`
* `/app/main.py`

If you are using pip to install dependencies your dockerfile could look like this-

```dockerfile
FROM ghcr.io/multi-py/python-gunicorn:py3.10-20.1.0

COPY requirements /requirements
RUN pip install --no-cache-dir -r /requirements
COPY ./app app
```

### PreStart Script

When the container is launched it will run the script at `/app/prestart.sh` before starting the gunicorn service. This is an ideal place to put things like database migrations.

## Python Versions

This project actively supports these Python versions:

* 3.10
* 3.9
* 3.8
* 3.7
* 3.6


## Image Variants

Like the upstream Python containers themselves a variety of image variants are supported.


### Full

The default container type, and if you're not sure what container to use start here. It has a variety of libraries and build tools installed, making it easy to extend.



### Slim

This container is similar to Full but with far less libraries and tools installed by default. If yo're looking for the tiniest possible image with the most stability this is your best bet.



### Alpine

This container is provided for those who wish to use Alpine. Alpine works a bit differently than the other image types, as it uses `musl` instead of `glibc` and many libaries are not well tested under `musl` at this time.



## Architectures

Every tag in this repository supports these architectures:

* linux/amd64
* linux/arm64
* linux/arm/v7


## Sponsorship

If you get use out of these containers please consider sponsoring me using Github!
<center>

[![Github Sponsorship](https://raw.githubusercontent.com/mechPenSketch/mechPenSketch/master/img/github_sponsor_btn.svg)](https://github.com/sponsors/tedivm)

</center>

## Tags
* Recommended Image: `ghcr.io/multi-py/python-gunicorn:py3.10-20.1.0`
* Slim Image: `ghcr.io/multi-py/python-gunicorn:py3.10-slim-20.1.0`

Tags are based on the package version, python version, and the upstream container the container is based on.

| gunicorn Version | Python Version | Full Container | Slim Container | Alpine Container |
|-----------------------|----------------|----------------|----------------|------------------|
| latest | 3.10 | py3.10-latest | py3.10-slim-latest | py3.10-alpine-latest |
| latest | 3.9 | py3.9-latest | py3.9-slim-latest | py3.9-alpine-latest |
| latest | 3.8 | py3.8-latest | py3.8-slim-latest | py3.8-alpine-latest |
| latest | 3.7 | py3.7-latest | py3.7-slim-latest | py3.7-alpine-latest |
| latest | 3.6 | py3.6-latest | py3.6-slim-latest | py3.6-alpine-latest |
| 20.1.0 | 3.10 | py3.10-20.1.0 | py3.10-slim-20.1.0 | py3.10-alpine-20.1.0 |
| 20.1.0 | 3.9 | py3.9-20.1.0 | py3.9-slim-20.1.0 | py3.9-alpine-20.1.0 |
| 20.1.0 | 3.8 | py3.8-20.1.0 | py3.8-slim-20.1.0 | py3.8-alpine-20.1.0 |
| 20.1.0 | 3.7 | py3.7-20.1.0 | py3.7-slim-20.1.0 | py3.7-alpine-20.1.0 |
| 20.1.0 | 3.6 | py3.6-20.1.0 | py3.6-slim-20.1.0 | py3.6-alpine-20.1.0 |
| 20.0.4 | 3.10 | py3.10-20.0.4 | py3.10-slim-20.0.4 | py3.10-alpine-20.0.4 |
| 20.0.4 | 3.9 | py3.9-20.0.4 | py3.9-slim-20.0.4 | py3.9-alpine-20.0.4 |
| 20.0.4 | 3.8 | py3.8-20.0.4 | py3.8-slim-20.0.4 | py3.8-alpine-20.0.4 |
| 20.0.4 | 3.7 | py3.7-20.0.4 | py3.7-slim-20.0.4 | py3.7-alpine-20.0.4 |
| 20.0.4 | 3.6 | py3.6-20.0.4 | py3.6-slim-20.0.4 | py3.6-alpine-20.0.4 |
| 20.0.3 | 3.10 | py3.10-20.0.3 | py3.10-slim-20.0.3 | py3.10-alpine-20.0.3 |
| 20.0.3 | 3.9 | py3.9-20.0.3 | py3.9-slim-20.0.3 | py3.9-alpine-20.0.3 |
| 20.0.3 | 3.8 | py3.8-20.0.3 | py3.8-slim-20.0.3 | py3.8-alpine-20.0.3 |
| 20.0.3 | 3.7 | py3.7-20.0.3 | py3.7-slim-20.0.3 | py3.7-alpine-20.0.3 |
| 20.0.3 | 3.6 | py3.6-20.0.3 | py3.6-slim-20.0.3 | py3.6-alpine-20.0.3 |
| 20.0.2 | 3.10 | py3.10-20.0.2 | py3.10-slim-20.0.2 | py3.10-alpine-20.0.2 |
| 20.0.2 | 3.9 | py3.9-20.0.2 | py3.9-slim-20.0.2 | py3.9-alpine-20.0.2 |
| 20.0.2 | 3.8 | py3.8-20.0.2 | py3.8-slim-20.0.2 | py3.8-alpine-20.0.2 |
| 20.0.2 | 3.7 | py3.7-20.0.2 | py3.7-slim-20.0.2 | py3.7-alpine-20.0.2 |
| 20.0.2 | 3.6 | py3.6-20.0.2 | py3.6-slim-20.0.2 | py3.6-alpine-20.0.2 |
| 20.0.0 | 3.10 | py3.10-20.0.0 | py3.10-slim-20.0.0 | py3.10-alpine-20.0.0 |
| 20.0.0 | 3.9 | py3.9-20.0.0 | py3.9-slim-20.0.0 | py3.9-alpine-20.0.0 |
| 20.0.0 | 3.8 | py3.8-20.0.0 | py3.8-slim-20.0.0 | py3.8-alpine-20.0.0 |
| 20.0.0 | 3.7 | py3.7-20.0.0 | py3.7-slim-20.0.0 | py3.7-alpine-20.0.0 |
| 20.0.0 | 3.6 | py3.6-20.0.0 | py3.6-slim-20.0.0 | py3.6-alpine-20.0.0 |
| 19.10.0 | 3.10 | py3.10-19.10.0 | py3.10-slim-19.10.0 | py3.10-alpine-19.10.0 |
| 19.10.0 | 3.9 | py3.9-19.10.0 | py3.9-slim-19.10.0 | py3.9-alpine-19.10.0 |
| 19.10.0 | 3.8 | py3.8-19.10.0 | py3.8-slim-19.10.0 | py3.8-alpine-19.10.0 |
| 19.10.0 | 3.7 | py3.7-19.10.0 | py3.7-slim-19.10.0 | py3.7-alpine-19.10.0 |
| 19.10.0 | 3.6 | py3.6-19.10.0 | py3.6-slim-19.10.0 | py3.6-alpine-19.10.0 |
| 19.9.0 | 3.10 | py3.10-19.9.0 | py3.10-slim-19.9.0 | py3.10-alpine-19.9.0 |
| 19.9.0 | 3.9 | py3.9-19.9.0 | py3.9-slim-19.9.0 | py3.9-alpine-19.9.0 |
| 19.9.0 | 3.8 | py3.8-19.9.0 | py3.8-slim-19.9.0 | py3.8-alpine-19.9.0 |
| 19.9.0 | 3.7 | py3.7-19.9.0 | py3.7-slim-19.9.0 | py3.7-alpine-19.9.0 |
| 19.9.0 | 3.6 | py3.6-19.9.0 | py3.6-slim-19.9.0 | py3.6-alpine-19.9.0 |
| 19.8.1 | 3.10 | py3.10-19.8.1 | py3.10-slim-19.8.1 | py3.10-alpine-19.8.1 |
| 19.8.1 | 3.9 | py3.9-19.8.1 | py3.9-slim-19.8.1 | py3.9-alpine-19.8.1 |
| 19.8.1 | 3.8 | py3.8-19.8.1 | py3.8-slim-19.8.1 | py3.8-alpine-19.8.1 |
| 19.8.1 | 3.7 | py3.7-19.8.1 | py3.7-slim-19.8.1 | py3.7-alpine-19.8.1 |
| 19.8.1 | 3.6 | py3.6-19.8.1 | py3.6-slim-19.8.1 | py3.6-alpine-19.8.1 |
| 19.8.0 | 3.10 | py3.10-19.8.0 | py3.10-slim-19.8.0 | py3.10-alpine-19.8.0 |
| 19.8.0 | 3.9 | py3.9-19.8.0 | py3.9-slim-19.8.0 | py3.9-alpine-19.8.0 |
| 19.8.0 | 3.8 | py3.8-19.8.0 | py3.8-slim-19.8.0 | py3.8-alpine-19.8.0 |
| 19.8.0 | 3.7 | py3.7-19.8.0 | py3.7-slim-19.8.0 | py3.7-alpine-19.8.0 |
| 19.8.0 | 3.6 | py3.6-19.8.0 | py3.6-slim-19.8.0 | py3.6-alpine-19.8.0 |
| 19.7.1 | 3.10 | py3.10-19.7.1 | py3.10-slim-19.7.1 | py3.10-alpine-19.7.1 |
| 19.7.1 | 3.9 | py3.9-19.7.1 | py3.9-slim-19.7.1 | py3.9-alpine-19.7.1 |
| 19.7.1 | 3.8 | py3.8-19.7.1 | py3.8-slim-19.7.1 | py3.8-alpine-19.7.1 |
| 19.7.1 | 3.7 | py3.7-19.7.1 | py3.7-slim-19.7.1 | py3.7-alpine-19.7.1 |
| 19.7.1 | 3.6 | py3.6-19.7.1 | py3.6-slim-19.7.1 | py3.6-alpine-19.7.1 |


### Older Tags

Older tags are left for historic purposes but do not receive updates. A full list of tags can be found on the package's [registry page](https://github.com/multi-py/python-gunicorn/pkgs/container/python-gunicorn).

## Environmental Variables

### `PORT`

The port that the application inside of the container will listen on. This is different from the host port that gets mapped to the container.


### `WORKERS`

The number of workers to launch. A good starting point is 4 processes per core (defaults to 4).


### `LOG_LEVEL`

The gunicorn log level. Must be one of the following:

* `critical`
* `error`
* `warning`
* `info`
* `debug`
* `trace`


### `MODULE_NAME`

The python module that gunicorn will import. This value is used to generate the APP_MODULE value.


### `VARIABLE_NAME`

The python variable containing the ASGI application inside of the module that gunicorn imports. This value is used to generate the APP_MODULE value.


### `APP_MODULE`

The python module and variable that is passed to gunicorn. When used the `VARIABLE_NAME` and `MODULE_NAME` environmental variables are ignored.


### `PRE_START_PATH`

Where to find the prestart script.


### `RELOAD`

When this is set to the string `true` gunicorn is launched in reload mode. If any files change gunicorn will reload the modules again, allowing for quick debugging. This comes at a performance cost, however, and should not be enabled on production machines.
