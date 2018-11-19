# tomcat8-docker

# Dockerfile

```
FROM tomcat
ENV JPDA_ADDRESS 8000
ENV JPDA_TRANSPORT dt_socket
RUN rm -rf /usr/local/tomcat/webapps/ROOT
COPY ./target/ROOT1.0.4.war /usr/local/tomcat/webapps/ROOT.war

ENTRYPOINT ["/usr/local/tomcat/bin/catalina.sh", "jpda", "run"]
EXPOSE 8088
```

# docker-compose.yml

```
web:
  image: tomcat
  ports:
    - "8000:8080/tcp"
    - "8002:8002/tcp"
  command: ["/usr/local/tomcat/bin/catalina.sh", "jpda", "run"]
  environment:
    JPDA_ADDRESS: 8002
    JPDA_TRANSPORT: dt_socket
  volumes:
    - ./target/ROOT1.0.4:/usr/local/tomcat/webapps/ROOT
```
