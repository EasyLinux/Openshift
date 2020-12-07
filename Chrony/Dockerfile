FROM alpine:3.12
LABEL author="Serge NOEL <serge.noel@easylinux.fr>"

RUN apk add --no-cache chrony

VOLUME /etc/chrony
EXPOSE 123/UDP
# ATTENTION : doit fonctionner en mode privileged 
CMD ["/usr/sbin/chronyd","-d"]
