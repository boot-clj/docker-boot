FROM bootclj/tooling AS build

WORKDIR /usr/src/bootstrap

RUN mkdir build bin src

COPY boot.properties build.boot ./

ENV BOOT_AS_ROOT=yes

RUN boot deps

ADD https://github.com/boot-clj/bootstrap/archive/master.tar.gz /usr/local/src/bootstrap-master.tar.gz

ADD /usr/local/src/bootstrap-master.tar.gz /usr/local/src/bootstrap

RUN boot build

RUN cat  src/head.sh target/loader.jar > bin/boot.sh

FROM bootclj/clojure:latest

COPY --from=build /usr/src/bootstrap/bin/boot.sh /usr/local/bin/boot

ENTRYPOINT ["boot"]
