FROM maven:3.6.3-jdk-8 as Build

RUN mkdir /app 
WORKDIR /app
RUN git clone --recursive https://github.com/OpenIdentityPlatform/OpenIDM.git
RUN sed -i 's/geolite.maxmind.com/geoip2.maxmind.com/g' /app/OpenIDM/OpenICF/OpenDJ/forgerock-parent/forgerock-commons/geo/pom.xml
RUN mvn -DskipTests -Dmaven.javadoc.skip=true clean install -f OpenIDM/OpenICF/OpenDJ/forgerock-parent
RUN mvn -DskipTests -Dmaven.javadoc.skip=true clean install -f OpenIDM/OpenICF/OpenDJ
#RUN mvn -DskipTests -Dmaven.javadoc.skip=true clean install -f OpenIDM/OpenICF 
#RUN mvn clean install -f OpenIDM

#FROM alpine:3.12
#LABEL author="Serge NOEL <serge.noel@easylinux.fr>"

#RUN mkdir /app 
#RUN apk add openjdk11-jre-headless
#COPY --from=Build \
#     OpenIDM/openidm-zip/target/openidm-*.zip \
#     /app
#WORKDIR /app
#RUN unzip openidm*

