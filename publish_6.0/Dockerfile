from centos:latest

RUN yum install wget -y

COPY aem6.0-publish-p4503.jar /AEM/aem/publish/aem6.0-publish-p4503.jar
COPY license.properties /AEM/aem/author/license.properties
COPY aem6 /etc/init.d/aem6

WORKDIR /AEM/aem/publish
RUN get --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u151-b12/e758a0de34e24606bca991d704f6dcbf/jdk-8u151-linux-x64.rpm"
RUN yum localinstall jdk-8u151-linux-x64.rpm -y
RUN java -jar aem6.0-publish-p4503.jar -unpack

RUN chkconfig --add aem6
RUN yum install initscripts -y
RUN yum update -y
RUN yum clean all

RUN chown -R $USER:$(id -G) /etc/init.d
RUN chmod 777 -R /etc/init.d/aem6

WORKDIR /AEM/aem/publish/crx-quickstart/bin
EXPOSE 4503 8001
RUN ./start
