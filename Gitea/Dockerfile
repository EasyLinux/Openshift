# Conteneur temporaire de compilation ppc64le
FROM alpine:3.12 As Build
LABEL author="Serge NOEL <serge.noel@easylinux.fr>"

# Chargement de pré-requis
RUN apk add git go npm nodejs build-base

# Récupération des sources 
RUN mkdir /app \
    && cd /app \
    && git clone https://github.com/go-gitea/gitea . 

# Compilation de Gitea 
WORKDIR /app
RUN TAGS="bindata" make build

# Contruction du runtime
FROM alpine:3.12
LABEL author="Serge NOEL <serge.noel@easylinux.fr>"

RUN apk add git sudo bash s6 openssh gettext \
    && mkdir /data \
    && adduser -g "Service Gitea" -D git   
COPY --from=Build /app/gitea /usr/local/bin/gitea
COPY Files/ /
RUN chown -R git: /etc/s6 
WORKDIR /data
VOLUME /data
USER git
EXPOSE 3000 22
ENV USER git
ENV GITEA_CUSTOM /data/gitea

CMD ["/app/gitea","web"] 
