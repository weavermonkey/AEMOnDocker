from centos:latest

COPY cq5-publish-p4503.jar /AEM/aem/publish/cq5-publish-p4503.jar
COPY license.properties /AEM/aem/publish/license.properties
RUN yum install initscripts -y
RUN yum install wget -y
RUN yum update -y
RUN yum clean all

WORKDIR /AEM/aem/publish
RUN wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u151-b12/e758a0de34e24606bca991d704f6dcbf/jdk-8u151-linux-x64.rpm"
RUN yum localinstall jdk-8u151-linux-x64.rpm -y
RUN java -jar cq5-publish-p4503.jar -unpack

WORKDIR /AEM/aem/publish/crx-quickstart/bin
COPY start /AEM/aem/publish/crx-quickstart/bin/start

COPY aem6 /etc/init.d/aem6
RUN chkconfig --add aem6
RUN chown -R $USER:$(id -G) /etc/init.d
RUN chmod 777 -R /etc/init.d/aem6

WORKDIR /AEM/aem/publish/crx-quickstart/bin
RUN cp quickstart quickstart.original
RUN cat quickstart.original | sed -e "s|4502|4503|g" -e "s|#CQ_RUNMODE=''|CQ_RUNMODE='publish'|g"  > quickstart

EXPOSE 4503
ENTRYPOINT ["/AEM/aem/publish/crx-quickstart/bin/quickstart", "-D", "FOREGROUND"]
