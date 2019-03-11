# base openjdk image
FROM bootclj/graalvm:latest

# clojure version
ARG CLOJURE_VERSION=1.10.0.411

# install clojure
RUN curl -L https://download.clojure.org/install/linux-install-${CLOJURE_VERSION}.sh -o install-cljs.sh

RUN chmod +x install-cljs.sh

RUN ./install-cljs.sh

RUN rm -rfv ./install-cljs.sh
#
