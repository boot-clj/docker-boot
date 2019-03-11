# base boot image
FROM bootclj/clojure:1.10.0-graalvm

# install leiningen
RUN curl -L https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein -o /usr/local/bin/lein

RUN chmod 755 /usr/local/bin/lein
#

# install latest boot
RUN curl -L https://github.com/boot-clj/boot-bin/releases/download/latest/boot.sh -o /usr/local/bin/boot

RUN chmod 755 /usr/local/bin/boot
#
