FROM ubuntu:14.04

MAINTAINER wangsh<462620215@qq.com>

ENV TOMCAT_MAJOR_VERSION 7
ENV TOMCAT_MINOR_VERSION 7.0.76

RUN sudo apt-get update \
    && sudo apt-get install -y openjdk-7-jdk \
    && sudo apt-get install -y openjdk-7-jre \
    && sudo apt-get install -y wget \
    && sudo apt-get install -y zip
 
RUN echo "export JAVA_HOME=/usr/lib/jvm/Java-7-openjdk-amd64">>/etc/profile
RUN echo "export JRE_HOME=$JAVA_HOME/jre">>/etc/profile
RUN echo "export CLASSPATH=$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH">>/etc/profile
RUN echo "export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$PATH">>/etc/profile

RUN sudo apt-get install -y subversion

WORKDIR /work

RUN wget http://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-${TOMCAT_MAJOR_VERSION}/v${TOMCAT_MINOR_VERSION}/bin/apache-tomcat-${TOMCAT_MINOR_VERSION}.zip \
     && unzip apache-tomcat*.zip && rm -f apache-tomcat*.zip && mv apache-tomcat* tomcat

RUN wget http://apache.mesi.com.ar/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.zip \
    && unzip apache-maven*.zip && rm -f apache-maven*.zip && mv apache-maven* maven

RUN echo "export M2_HOME=/work/maven">>/etc/profile
RUN echo "export PATH=$M2_HOME/bin:$PATH">>/etc/profile

COPY ./settings.xml /root/.m2/

COPY ./docker-entrypoint.sh /

RUN ["chmod", "+x", "/docker-entrypoint.sh"]

EXPOSE 8080

ENTRYPOINT ["/docker-entrypoint.sh"]
