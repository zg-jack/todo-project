FROM java:8

WORKDIR /app
COPY TodoDemo.jar /app/TodoDemo.jar
RUN useradd -ms /bin/bash admin && chown admin:admin TodoDemo.jar && bash -c 'touch TodoDemo.jar'
USER admin
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","TodoDemo.jar"]
