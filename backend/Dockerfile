FROM hub.agoralab.co/adc/openjdk:11-alpine

#镜像的制作人
MAINTAINER caitengwen@agora.io

#工作目录
WORKDIR /app

#在容器中创建挂载点，可以多个
VOLUME ["/app/logs","/app/tmp"]

#声明了容器应该打开的端口并没有实际上将它打开
EXPOSE 8080

#定义参数
ARG JAR_FILE=target/backend-1.9.jar
ARG PROFILES
ARG CLUSTER
ARG JVM_OPT
ENV PROFILES=${PROFILES}
ENV CLUSTER=${CLUSTER}
ENV JVM_OPT="${JVM_OPT}"



#拷贝本地文件到镜像中
COPY ${JAR_FILE} app.jar
COPY src/main/resources/jmeter/bin/jmeter.properties /opt/jmeter/bin/jmeter.properties

#RUN apk add --no-cache redis

#JVM_OPT公共的jvm参数
ENTRYPOINT java -jar -Dspring.profiles.active=$PROFILES -Dconfig.path=/opt/metersphere/conf/metersphere.properties ${JVM_OPT//%s/ } app.jar
