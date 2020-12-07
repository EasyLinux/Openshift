FROM alpine:3.12
LABEL author="Serge NOEL <serge.noel@easylinux.fr>"

RUN apk add openjdk8-jre fontconfig\
    && adduser -g "Jenkins User" -D jenkins

# Copie de la fonte manquante
RUN mkdir -p /usr/share/fonts/TTF/ \
    && cd /usr/share/fonts/TTF/ \ 
    && wget http://thorpora.fr/wp-content/uploads/2017/01/DejaVuSerif.zip \
    && unzip DejaVuSerif.zip \
    && rm DejaVuSerif.zip

# Copie de Jenkins
RUN mkdir /app \
    && cd /app \
    && wget https://get.jenkins.io/war-stable/2.249.2/jenkins.war

USER jenkins      
WORKDIR /home/jenkins
VOLUME /home/jenkins
ENV JENKINS_HOME=/home/jenkins 

CMD ["java","-Djava.awt.headless=true","-jar","/app/jenkins.war"] 
