FROM alpine:3.12
LABEL author="Serge NOEL <serge.noel@easylinux.fr>"

RUN apk add --no-cache postfix postfix-ldap \
    && addgroup -g 5000 vmail 
RUN sed -i "s|vmail:x:101:102:vmail:/var/mail/domains:/sbin/nologin|vmail:x:5000:5000:vmail:/var/mail/domains:/sbin/nologin|g" /etc/passwd \
    && chown vmail: /var/mail  

VOLUME /var/mail /etc/postfix
EXPOSE 25

RUN apk add busybox-extras nano mc


