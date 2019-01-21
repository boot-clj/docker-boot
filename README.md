# docker-boot
Official boot-clj docker images.

## bootclj/openjdk

```
FROM bootclj/openjdk AS openjdk
```

This is our base openjdk image, we include a few build tools (bash, curl, build-base/build-essentials) to make the developer experience a bit more enjoyable.

`openjdk:8-alpine -> bootclj/openjdk`

## bootclj/clojure

```
FROM bootclj/clojure AS clojure
```

Our clojure image is built to include Clojure [Deps and Cli](https://clojure.org/reference/deps_and_cli). This provides developers with a complete image for running clojure.

`bootclj/openjdk -> bootclj/clojure`

## bootclj/tooling

```
FROM bootclj/tooling AS tools
```

The build tooling image is provided as a convenience for developers looking to build clojure projects, it is built on top of the clojure image and includes the latest versions of boot and lein.

`bootclj/clojure -> bootclj/tooling`
