FROM alpine:3.12
LABEL author="Serge NOEL <serge.noel@easylinux.fr>"

RUN apk add openjdk8 \
    && mkdir /app
WORKDIR /app
RUN wget https://downloads.graylog.org/releases/graylog/graylog-3.3.8.tgz \
    && tar zxvf  graylog-3.3.8.tgz \
    && rm  graylog-3.3.8.tgz

COPY Files/ /
VOLUME /etc/graylog 
EXPOSE 9000
CMD /usr/local/bin/launch:q
