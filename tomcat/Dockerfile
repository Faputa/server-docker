FROM openjdk:6-jdk

RUN curl -SL https://archive.apache.org/dist/tomcat/tomcat-6/v6.0.9/bin/apache-tomcat-6.0.9.tar.gz | tar xz -C /usr/local;\
    ln -s /usr/local/apache-tomcat-6.0.9 /usr/local/tomcat

WORKDIR /usr/local/tomcat/bin
EXPOSE 8080
CMD [ "./catalina.sh", "run" ]