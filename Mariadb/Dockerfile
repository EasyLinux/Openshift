FROM alpine:3.13
LABEL author="Serge NOEL <serge.noel@easylinux.fr>" 

RUN apk add mariadb mariadb-client \
    && sed -i "s/skip-networking/# skip-networking/g" /etc/my.cnf.d/mariadb-server.cnf \
    && sed -i "s/#bind-address=0.0.0.0 /bind-address=0.0.0.0/g" /etc/my.cnf.d/mariadb-server.cnf 
     
COPY Files/ /
EXPOSE 3306
VOLUME /var/lib/mysql

USER mysql
CMD ["/usr/local/bin/launch"]
 
