FROM alpine:3.13
LABEL autrho="Serge NOEL <serge.noel@easylinux.fr>"

RUN apk add git go build-base bash
RUN mkdir ~/go
# ARG GOPATH="/root/go"
# ENV GOPATH="/root/go"
RUN mkdir -p /root/go/src/github.com/operator-framework
WORKDIR /root/go/src/github.com/operator-framework
RUN git clone https://github.com/operator-framework/operator-sdk
WORKDIR /root/go/src/github.com/operator-framework/operator-sdk
RUN git checkout master
RUN make install
# ARG PATH=$PATH:$(go env GOPATH)/bin
# ENV PATH=$PATH:$(go env GOPATH)/bin
RUN mkdir /app
WORKDIR /app

