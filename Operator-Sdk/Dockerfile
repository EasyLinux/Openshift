FROM alpine:3.13
LABEL author="Serge NOEL <serge.noel@easylinux.fr>"

COPY Files/ /
RUN apk add git go build-base bash 
RUN mkdir /root/go
RUN mkdir -p /root/go/src/github.com/operator-framework
WORKDIR /root/go/src/github.com/operator-framework
RUN git clone https://github.com/operator-framework/operator-sdk
WORKDIR /root/go/src/github.com/operator-framework/operator-sdk
RUN git checkout master
RUN make install
RUN mkdir /app
WORKDIR /app
RUN rm /etc/apk/repositories
RUN mv /etc/apk/repositories.old /etc/pak/repositories
RUN apk update
RUN apk add kubectl

VOLUME /root/.kube /app
