# base boot image
FROM bootclj/tooling as build

ARG VERSION=3.0.0-SNAPSHOT

WORKDIR /usr/local/src

RUN git clone https://github.com/boot-clj/boot.git

WORKDIR /usr/local/src/boot

# base
WORKDIR /usr/local/src/boot-clj/boot/base

RUN mvn -q install

# pod
WORKDIR /usr/local/src/boot-clj/boot/pod

RUN lein install

# aether
WORKDIR /usr/local/src/boot-clj/boot/aether

RUN lein install

RUN lein uberjar

RUN cp target/aether-3.0.0-SNAPSHOT-standalone.jar /usr/local/src/boot-clj/boot/base/src/main/resources/aether.uber.jar

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

RUN mvn -q assembly:assembly -DdescriptorId=uberjar

# boot jar
WORKDIR /usr/local/src/boot-clj/boot/boot

RUN lein install

# final artifact
WORKDIR /usr/local/src/boot-clj

RUN mkdir -p bin

RUN cp boot/base/target/base-3.0.0-SNAPSHOT-uberjar.jar bin/boot.uber.jar

FROM bootclj/bootstrap AS bootstrap

FROM bootclj/clojure:latest

COPY --from=build /usr/local/src/boot-clj/bin/boot.uber.jar ~/.boot/cache/bin/3.0.0-SNAPSHOT/boot.jar

COPY --from=bootstrap /usr/local/bin/boot /usr/local/bin/boot

RUN boot -V

ENTRYPOINT ["boot"]
