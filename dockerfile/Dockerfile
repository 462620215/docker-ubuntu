FROM ubuntu:14.04

MAINTAINER wangsh<462620215@qq.com>

ENV TOMCAT_MAJOR_VERSION 7
ENV TOMCAT_MINOR_VERSION 7.0.82

RUN sudo rm -f /etc/localtime \
    && sudo ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

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

RUN wget http://brandpano-test.oss-cn-shenzhen.aliyuncs.com/docker-github/settings.xml \
    && mkdir -p /root/.m2/ && mv settings.xml /root/.m2/
    
RUN wget http://brandpano-test.oss-cn-shenzhen.aliyuncs.com/docker-github/java.security \
    && mv java.security /usr/lib/jvm/java-1.7.0-openjdk-amd64/jre/lib/security/
    
RUN wget http://brandpano-test.oss-cn-shenzhen.aliyuncs.com/docker-github/docker-entrypoint.sh \
    && mkdir /work && mv docker-entrypoint.sh /work/

RUN ["chmod", "+x", "/work/docker-entrypoint.sh"]

WORKDIR /work

RUN wget http://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-${TOMCAT_MAJOR_VERSION}/v${TOMCAT_MINOR_VERSION}/bin/apache-tomcat-${TOMCAT_MINOR_VERSION}.zip \
     && unzip apache-tomcat*.zip && rm -f apache-tomcat*.zip && mv apache-tomcat* tomcat

RUN wget http://mirror.bit.edu.cn/apache/maven/maven-3/3.5.0/binaries/apache-maven-3.5.0-bin.zip \
    && unzip apache-maven*.zip && rm -f apache-maven*.zip && mv apache-maven* maven

RUN echo "export M2_HOME=/work/maven">>/etc/profile
RUN echo "export PATH=$M2_HOME/bin:$PATH">>/etc/profile

RUN pwd
RUN ls

EXPOSE 8080

ENTRYPOINT ["/work/docker-entrypoint.sh"]

