# base boot image
FROM bootclj/clojure:graalvm

# install leiningen
RUN curl https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein -o /usr/local/bin/lein

RUN chmod 755 /usr/local/bin/lein
#

# install latest boot
RUN curl https://github.com/boot-clj/boot-bin/releases/download/latest/boot.sh -o /usr/local/bin/boot

RUN chmod 755 /usr/local/bin/boot
#
