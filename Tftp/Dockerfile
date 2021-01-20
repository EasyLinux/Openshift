FROM alpine:3.12
LABEL author="Serge NOEL <serge.noe@easylinux.fr>"

RUN apk add tftp-hpa

VOLUME /var/tftp
EXPOSE 69/UDP
CMD echo -n "Starting " && in.tftpd --version && in.tftpd -L --secure -vv /var/tftp
