FROM alpine:3.12
LABEL author="Serge NOEL <serge.noel@easylinux.fr>"

RUN apk add php7-apache2 php7-intl php7-openssl php7-pdo_mysql php7-mbstring php7-ldap php7-session php7-gd php7-xmlwriter php7-mysqli

RUN sed -i 's/Listen 80/Listen 8080/g' /etc/apache2/httpd.conf \
    && sed -i 's|/var/www/localhost/htdocs|/var/www/html|g' /etc/apache2/httpd.conf \
    && sed -i 's|logs/error.log|/dev/stderr|g' /etc/apache2/httpd.conf \
    && sed -i 's|logs/access.log|/dev/stdout|g' /etc/apache2/httpd.conf \
    && mkdir -p /run/apache2 \
    && chmod 777 /run/apache2  

EXPOSE 8080
VOLUME /var/www/html
CMD ["/usr/sbin/httpd","-D","FOREGROUND"]     

