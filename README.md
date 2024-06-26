# python-gunicorn


A multiarchitecture container image for running Python with Gunicorn.

Looking for the containers? [Head over to the Github Container Registry](https://github.com/multi-py/python-gunicorn/pkgs/container/python-gunicorn)!

<!--ts-->
* [python-gunicorn](#python-gunicorn)
   * [Benefits](#benefits)
      * [Multi Architecture Builds](#multi-architecture-builds)
      * [Small Images via Multi Stage Builds](#small-images-via-multi-stage-builds)
      * [No Rate Limits](#no-rate-limits)
      * [Rapid Building of New Versions](#rapid-building-of-new-versions)
      * [Regular Updates](#regular-updates)
   * [How To](#how-to)
      * [Using the Full Image](#using-the-full-image)
      * [Using the Slim Image](#using-the-slim-image)
      * [Using the Alpine Image](#using-the-alpine-image)
      * [Copy Just the Packages](#copy-just-the-packages)
      * [Add Your App](#add-your-app)
      * [PreStart Script](#prestart-script)
   * [Environmental Variables](#environmental-variables)
      * [PORT](#port)
      * [WORKERS](#workers)
      * [LOG_LEVEL](#log_level)
      * [MODULE_NAME](#module_name)
      * [VARIABLE_NAME](#variable_name)
      * [APP_MODULE](#app_module)
      * [PRE_START_PATH](#pre_start_path)
      * [RELOAD](#reload)
      * [GUNICORN_EXTRA_FLAGS](#gunicorn_extra_flags)
   * [Python Versions](#python-versions)
   * [Image Variants](#image-variants)
      * [Full](#full)
      * [Slim](#slim)
      * [Alpine](#alpine)
   * [Architectures](#architectures)
   * [Sponsorship](#sponsorship)
   * [Tags](#tags)
      * [Older Tags](#older-tags)
<!--te-->

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

### Using the Full Image
The Full Images use the base Python Docker images as their parent. These images are based off of Ubuntu and contain a variety of build tools.

To pull the latest full version:

```bash
docker pull ghcr.io/multi-py/python-gunicorn:py3.12-LATEST
```

To include it in the dockerfile instead:

```dockerfile
FROM ghcr.io/multi-py/python-gunicorn:py3.12-LATEST
```

### Using the Slim Image

The Slim Images use the base Python Slim Docker images as their parent. These images are very similar to the Full images, but without the build tools. These images are much smaller than their counter parts but are more difficult to compile wheels on.

To pull the latest slim version:

```bash
docker pull ghcr.io/multi-py/python-gunicorn:py3.12-slim-LATEST
```

To include it in the dockerfile instead:

```dockerfile
FROM ghcr.io/multi-py/python-gunicorn:py3.12-slim-LATEST
```



### Using the Alpine Image

The Alpine Images use the base Python Alpine Docker images as their parent. These images use Alpine as their operating system, with musl instead of glibc.

In theory these images are smaller than even the slim images, but this amounts to less than 30mb difference. Additional Python libraries tend not to be super well tested on Alpine. These images should be used with care and testing until this ecosystem matures.


To pull the latest alpine version:

```bash
docker pull ghcr.io/multi-py/python-gunicorn:py3.12-alpine-LATEST
```

To include it in the dockerfile instead:

```dockerfile
FROM ghcr.io/multi-py/python-gunicorn:py3.12-alpine-LATEST
```




### Copy Just the Packages
It's also possible to copy just the Python packages themselves. This is particularly useful when you want to use the precompiled libraries from multiple containers.

```dockerfile
FROM python:3.12

COPY --from=ghcr.io/multi-py/python-gunicorn:py3.12-slim-LATEST /usr/local/lib/python3.12/site-packages/* /usr/local/lib/python3.12/site-packages/
```

### Add Your App

By default the startup script checks for the following packages and uses the first one it can find-

* `/app/app/main.py`
* `/app/main.py`

If you are using pip to install dependencies your dockerfile could look like this-

```dockerfile
FROM ghcr.io/multi-py/python-gunicorn:py3.12-22.0.0

COPY requirements /requirements
RUN pip install --no-cache-dir -r /requirements
COPY ./app app
```

### PreStart Script

When the container is launched it will run the script at `/app/prestart.sh` before starting the gunicorn service. This is an ideal place to put things like database migrations.

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


### `GUNICORN_EXTRA_FLAGS`

This variable can be used to pass extra flags to the `gunicorn` command on launch. It's value is added directly to the command that is called, and has to be formatted appropriately for the command line.

## Python Versions

This project actively supports these Python versions:

* 3.12
* 3.11
* 3.10
* 3.9
* 3.8


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
* Recommended Image: `ghcr.io/multi-py/python-gunicorn:py3.12-22.0.0`
* Slim Image: `ghcr.io/multi-py/python-gunicorn:py3.12-slim-22.0.0`

Tags are based on the package version, python version, and the upstream container the container is based on.

| gunicorn Version | Python Version | Full Container | Slim Container | Alpine Container |
|-----------------------|----------------|----------------|----------------|------------------|
| latest | 3.12 | py3.12-latest | py3.12-slim-latest | py3.12-alpine-latest |
| latest | 3.11 | py3.11-latest | py3.11-slim-latest | py3.11-alpine-latest |
| latest | 3.10 | py3.10-latest | py3.10-slim-latest | py3.10-alpine-latest |
| latest | 3.9 | py3.9-latest | py3.9-slim-latest | py3.9-alpine-latest |
| latest | 3.8 | py3.8-latest | py3.8-slim-latest | py3.8-alpine-latest |
| 22.0.0 | 3.12 | py3.12-22.0.0 | py3.12-slim-22.0.0 | py3.12-alpine-22.0.0 |
| 22.0.0 | 3.11 | py3.11-22.0.0 | py3.11-slim-22.0.0 | py3.11-alpine-22.0.0 |
| 22.0.0 | 3.10 | py3.10-22.0.0 | py3.10-slim-22.0.0 | py3.10-alpine-22.0.0 |
| 22.0.0 | 3.9 | py3.9-22.0.0 | py3.9-slim-22.0.0 | py3.9-alpine-22.0.0 |
| 22.0.0 | 3.8 | py3.8-22.0.0 | py3.8-slim-22.0.0 | py3.8-alpine-22.0.0 |
| 21.2.0 | 3.12 | py3.12-21.2.0 | py3.12-slim-21.2.0 | py3.12-alpine-21.2.0 |
| 21.2.0 | 3.11 | py3.11-21.2.0 | py3.11-slim-21.2.0 | py3.11-alpine-21.2.0 |
| 21.2.0 | 3.10 | py3.10-21.2.0 | py3.10-slim-21.2.0 | py3.10-alpine-21.2.0 |
| 21.2.0 | 3.9 | py3.9-21.2.0 | py3.9-slim-21.2.0 | py3.9-alpine-21.2.0 |
| 21.2.0 | 3.8 | py3.8-21.2.0 | py3.8-slim-21.2.0 | py3.8-alpine-21.2.0 |
| 21.1.0 | 3.12 | py3.12-21.1.0 | py3.12-slim-21.1.0 | py3.12-alpine-21.1.0 |
| 21.1.0 | 3.11 | py3.11-21.1.0 | py3.11-slim-21.1.0 | py3.11-alpine-21.1.0 |
| 21.1.0 | 3.10 | py3.10-21.1.0 | py3.10-slim-21.1.0 | py3.10-alpine-21.1.0 |
| 21.1.0 | 3.9 | py3.9-21.1.0 | py3.9-slim-21.1.0 | py3.9-alpine-21.1.0 |
| 21.1.0 | 3.8 | py3.8-21.1.0 | py3.8-slim-21.1.0 | py3.8-alpine-21.1.0 |
| 21.0.1 | 3.12 | py3.12-21.0.1 | py3.12-slim-21.0.1 | py3.12-alpine-21.0.1 |
| 21.0.1 | 3.11 | py3.11-21.0.1 | py3.11-slim-21.0.1 | py3.11-alpine-21.0.1 |
| 21.0.1 | 3.10 | py3.10-21.0.1 | py3.10-slim-21.0.1 | py3.10-alpine-21.0.1 |
| 21.0.1 | 3.9 | py3.9-21.0.1 | py3.9-slim-21.0.1 | py3.9-alpine-21.0.1 |
| 21.0.1 | 3.8 | py3.8-21.0.1 | py3.8-slim-21.0.1 | py3.8-alpine-21.0.1 |
| 21.0.0 | 3.12 | py3.12-21.0.0 | py3.12-slim-21.0.0 | py3.12-alpine-21.0.0 |
| 21.0.0 | 3.11 | py3.11-21.0.0 | py3.11-slim-21.0.0 | py3.11-alpine-21.0.0 |
| 21.0.0 | 3.10 | py3.10-21.0.0 | py3.10-slim-21.0.0 | py3.10-alpine-21.0.0 |
| 21.0.0 | 3.9 | py3.9-21.0.0 | py3.9-slim-21.0.0 | py3.9-alpine-21.0.0 |
| 21.0.0 | 3.8 | py3.8-21.0.0 | py3.8-slim-21.0.0 | py3.8-alpine-21.0.0 |


### Older Tags

Older tags are left for historic purposes but do not receive updates. A full list of tags can be found on the package's [registry page](https://github.com/multi-py/python-gunicorn/pkgs/container/python-gunicorn).

