FROM alpine:3.13
LABEL author="Serge NOEL <serge.noel@easylinux.fr>"

# Installation des pré-requis
RUN apk add php7-apache2 php7-intl php7-openssl php7-pdo_mysql php7-mbstring php7-ldap \
    php7-session php7-gd php7-xmlwriter php7-mysqli php7-json php7-ctype \
    php7-iconv php7-curl php7-simplexml php7-pecl-apcu php7-opcache \
    php7-xmlrpc php7-exif php7-zip php7-bz2 php7-fileinfo php7-sodium

# Ecoute sur le port 8080 (80 est un port réservé)
# Documents dans /var/www/html
# Renvoi des erreurs sur la console
RUN sed -i 's/Listen 80/Listen 8080/g' /etc/apache2/httpd.conf \
    && sed -i 's|/var/www/localhost/htdocs|/var/www/html|g' /etc/apache2/httpd.conf \
    && sed -i 's|logs/error.log|/dev/stderr|g' /etc/apache2/httpd.conf \
    && sed -i 's|logs/access.log|/dev/stdout|g' /etc/apache2/httpd.conf \
    && mkdir -p /run/apache2 \
    && chmod 777 /run/apache2 \
    && mkdir /var/www/html \
    && cd /var/www/html \
    && wget https://github.com/glpi-project/glpi/releases/download/9.5.5/glpi-9.5.5.tgz \
    && tar zxf glpi-9.5.5.tgz --strip 1 \
    && rm glpi-9.5.5.tgz
WORKDIR /var/www/html
COPY Files/ /
RUN chown -R root: /var/www/html \
    && cp -r /var/www/html/files/* /var/lib/glpi/ \
    && chmod -R 777 /var/lib/glpi \
    && chmod 777 /etc/glpi \
    && chmod -R 777 /var/log/glpi

EXPOSE 8080
VOLUME /var/lib/glpi /etc/glpi
CMD ["/usr/sbin/httpd","-D","FOREGROUND"]