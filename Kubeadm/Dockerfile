FROM alpine:3.12

RUN apk add go  git \
    && mkdir /app

WORKDIR /app 

RUN git clone https://github.com/kubernetes/kubernetes

WORKDIR /app/kubernetes/cmd/kubeadm
RUN go build

WORKDIR /app/kubernetes/cmd/kubectl
RUN go build

WORKDIR /app/kubernetes/cmd/kubelet
RUN go build

WORKDIR /app/kubernetes/cmd/kube-apiserver
RUN go build

WORKDIR /app/kubernetes/cmd/kube-controller-manager
RUN go build

WORKDIR /app/kubernetes/cmd/kube-proxy
RUN go build

WORKDIR /app/kubernetes/cmd/kube-scheduler
RUN go build
