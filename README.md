# Buildpack for Chromium

This project is a Scalingo buildpack for using `chrome` in your project.

It doesn't do anything else, you have to use it alongside another buildpack
thanks to the [multi-buildpack](https://github.com/Scalingo/multi-buildpack).

This buildpack provides a static build of the latest Linux build of Chromium
downloaded from https://www.googleapis.com/

Usage
-----

## Setup the multi-buildpack

To use this buildpack, you should prepare a `.buildpacks` file that contains
this buildpack url and your real buildpack url.

```sh
$ cat .buildpacks
https://github.com/Scalingo/chromium-buildpack.git
https://github.com/Scalingo/apt-buildpack.git
https://github.com/Scalingo/ruby-buildpack.git
```

The first buildpack will install chromium, the second will install dependencies from your `Aptfile` and the final one will handle the deployment of your
application, here using Ruby. For any other technology, check out
[http://doc.scalingo.com/buildpacks/](http://doc.scalingo.com/buildpacks/).

## List apt dependencies

Chromium requires you use the `apt-buildpack` to install extra libraries. Create
an `Aptfile` at the root of your application with the following:

```sh
# Chromium dependencies
libasound2
libatk-bridge2.0-0
libatk1.0-0
libdrm2
libgbm1
libgtk-3-0
libnss3
libx11-xcb1
libxcb-dri3-0
libxcomposite1
libxcursor1
libxdamage1
libxi6
libxrandr2
libxss1
```

## Setup your application configuration

```sh
$ scalingo env-set BUILDPACK_URL=https://github.com/Scalingo/multi-buildpack.git
$ git push scalingo master
```

You can verify Chrome is installed with the following command.

```
$ scalingo run "/app/vendor/chrome-linux/chrome --version"
```
