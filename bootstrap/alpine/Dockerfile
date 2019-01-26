FROM bootclj/tooling AS build

WORKDIR /usr/src/bootstrap

RUN mkdir build bin src

COPY boot.properties build.boot ./

ENV BOOT_AS_ROOT=yes

RUN boot deps

COPY . .

RUN boot build

RUN cat  src/head.sh target/loader.jar > bin/boot.sh

FROM bootclj/clojure:latest

COPY --from=build /usr/src/bootstrap/bin/boot.sh /usr/local/bin/boot

ENTRYPOINT ["boot"]
