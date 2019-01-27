FROM bootclj/tooling AS build

WORKDIR /usr/local/src

RUN git clone https://github.com/boot-clj/bootstrap.git

WORKDIR /usr/local/src/bootstrap

RUN mkdir -p bin

ENV BOOT_AS_ROOT=yes

RUN boot deps

RUN boot build

RUN cat src/head.sh target/loader.jar > bin/boot.sh

FROM bootclj/clojure:latest

COPY --from=build /usr/local/src/bootstrap/bin/boot.sh /usr/local/bin/boot

ENTRYPOINT ["boot"]
