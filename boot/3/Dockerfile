# base boot image
FROM bootclj/tooling as build

ARG VERSION=3.0.0-SNAPSHOT

WORKDIR /usr/local/src

RUN git clone https://github.com/boot-clj/boot.git boot-clj

WORKDIR /usr/local/src/boot-clj

RUN git checkout ${VERSION}

# base
WORKDIR /usr/local/src/boot-clj/boot/base

RUN lein install

# pod
WORKDIR /usr/local/src/boot-clj/boot/pod

RUN lein install

# aether
WORKDIR /usr/local/src/boot-clj/boot/aether

RUN lein install

RUN lein uberjar

RUN cp target/aether-${VERSION}-standalone.jar ../base/src/main/resources/aether.uber.jar

# worker
WORKDIR /usr/local/src/boot-clj/boot/worker

RUN lein install

# core
WORKDIR /usr/local/src/boot-clj/boot/core

RUN lein install

# tasks
WORKDIR /usr/local/src/boot-clj/boot/tasks

RUN lein install

# base uber
WORKDIR /usr/local/src/boot-clj/boot/base

RUN lein uberjar

# boot jar
WORKDIR /usr/local/src/boot-clj/boot/boot

RUN lein install

# final artifact
WORKDIR /usr/local/src/boot-clj

RUN mkdir -p bin

RUN cp boot/base/target/base-${VERSION}-standalone.jar bin/boot.uber.jar

FROM bootclj/bootstrap AS bootstrap

FROM bootclj/clojure:latest

COPY --from=build /usr/local/src/boot-clj/bin/boot.uber.jar ~/.boot/cache/bin/${VERSION}/boot.jar

COPY --from=bootstrap /usr/local/bin/boot /usr/local/bin/boot

RUN chmod +x /usr/local/bin/boot

RUN boot -V

ENTRYPOINT ["boot"]
