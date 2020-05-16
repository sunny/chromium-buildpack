# Buildpack for chromium

This project is a Scalingo buildpack for using Chrome in your project.

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
https://github.com/Scalingo/ruby-buildpack.git 
```

The first buildpack will install Chrome, the second will handle the deployment
of your go application. For any other technology,
go to [http://doc.scalingo.com/buildpacks/](http://doc.scalingo.com/buildpacks/)

## Setup your application configuration
    
```sh
$ scalingo env-set BUILDPACK_URL=https://github.com/Scalingo/multi-buildpack.git
$ git push scalingo master

```

You can verify installing Chrome with the following command.

```
$ scalingo run "/app/vendor/chrome-linux/chrome --version"
```
