# Dart webdev Docker image

Web development with Dart 2 and `webdev`, see https://webdev.dartlang.org/guides/get-started.

Built based on https://hub.docker.com/r/google/dart/.

## Description

Use [Dart's `webdev` tool](https://webdev.dartlang.org/tools/webdev) to build, serve and test web apps, without installing Dart locally.

## Build

```shell
$ docker build -t martingregoire/dart-webdev .
```

## Push to Docker hub
```shell
$ docker push martingregoire/dart-webdev
```

## Usage

### App creation

To create a web app, use one of the templates provided by [stagehand](https://pub.dartlang.org/packages/stagehand), like `web-simple` in the following example:

```shell
$ docker run --rm -it -v $PWD:/app -p 8080:8080 -w /app martingregoire/dart-webdev stagehand web-simple
```

---

This creates an app based on the `web-simple` template in the current directory.

Note: due to Docker volume mounting, the created files may belong the `root` user (depending on your system setup). If your IDE complains that it cannot write to the created files, `chown` the files to your user like this:

```shell
$ chown -R $(id -u) .
```

### App development

To start development, fire up the container, install pub packages, and start `webdev`, all in one line:

```shell
$ docker run --rm -it -v $PWD:/app -p 8080:8080 -w /app martingregoire/dart-webdev webdev-serve
```

---

Start a browser and connect to http://localhost:8080, where you should see `webdev` serving your web app. Live reloading is enabled, so anytime you change a source file and save, your browser should automatically reload the page.

Note: if you add any pub packages, you have to restart the container using the above command!

---

Alternatively you can use the container like this, allowing you to manually e.g. install pub packages:

```shell
$ docker run -it -v $PWD:/app -p 8080:8080 -w /app martingregoire/dart-webdev
```

---

Then inside container, run e.g:

```shell
root@...:/app# pub get
```

---

Or to start `webdev`:

```shell
root@...:/app# webdev serve --hostname 0.0.0.0 --live-reload
```
