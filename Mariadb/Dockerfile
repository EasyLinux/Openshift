FROM  debian:buster
LABEL author="Serge NOEL <serge.noel@easylinux.fr>" \
      app="MariaDb" 

RUN apt-get update \
    && apt-get install -y mariadb-server \
    && sed -i "s/127.0.0.1/0.0.0.0/g" /etc/mysql/mariadb.conf.d/50-server.cnf
COPY Files/ /
EXPOSE 3306
VOLUME /var/lib/mysql

CMD ["/usr/local/bin/launch"]
 
