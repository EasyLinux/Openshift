FROM alpine:3.12
LABEL author="Serge NOEL <serge.noel@easylinux.fr>" 

RUN apk add mariadb-client bash \
    && mkdir /app

WORKDIR /app     
     
COPY Files/ /
VOLUME /app

ENTRYPOINT ["/usr/local/bin/launch"]
 