FROM alpine:3.7

RUN apk update && apk add gcc autoconf automake bash musl-dev make git openssh-client

RUN ( \
    mkdir -p /src/cronie && \
    cd /src && \
    git clone https://github.com/0xbad0c0d3/cronie.git && \
    cd /src/cronie && \
    bash ./autogen.sh && ./configure --sysconfdir=/etc --without-pam --without-selinux && make && make install && make clean && \
    cd / && rm -rf /src/cronie \
)

VOLUME ["/usr/local/var/spool/cron", "/etc/cron.d"]

CMD ["crond", "-n", "-s", "-x", "proc"]
