# Image temporaire de compilation MongoDB
FROM debian:buster AS Build
LABEL author="Serge NOEL <serge.noel@easylinux.fr>"

RUN apt-get update
RUN apt-get install -y build-essential python3 python3-pip libcurl4-openssl-dev git
RUN apt-get install -y libssl-dev

RUN mkdir /app
WORKDIR /app

RUN echo "Récupérer les sources"
RUN git clone https://github.com/mongodb/mongo .

RUN echo "Installer les dépendances python"
RUN python3 -m pip install -r etc/pip/compile-requirements.txt

RUN echo "Compiler mongod"
RUN python3 buildscripts/scons.py install-mongod

FROM debian:buster
RUN apt-get update
RUN apt-get install libcurl4
COPY --from=Build mogod /usr/local/bin/mongod  

VOLUME /data/db /etc/mongod
EXPOSE 27017

CMD ["/usr/local/bin/mongod","-f","/etc/mongod/mongod.conf"] 

