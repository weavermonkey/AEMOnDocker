from centos:latest


COPY aem6.0-author-p4502.jar /AEM/aem/author/aem6.0-author-p4502.jar
COPY license.properties /AEM/aem/author/license.properties
COPY aem6 /etc/init.d/aem6

RUN yum install wget -y
RUN yum install initscripts -y
RUN wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u151-b12/e758a0de34e24606bca991d704f6dcbf/jdk-8u151-linux-x64.rpm"
RUN yum localinstall jdk-8u151-linux-x64.rpm -y

WORKDIR /AEM/aem/author
RUN java -jar aem6.0-author-p4502.jar -unpack

RUN chkconfig --add aem6
RUN yum update -y
RUN yum clean all

RUN chown -R $USER:$(id -G) /etc/init.d
RUN chmod 777 -R /etc/init.d/aem6

#editing quickstart to set runmode to author
WORKDIR /AEM/aem/author/crx-quickstart/bin
RUN cp quickstart quickstart.original
RUN cat quickstart.original | sed "s|#CQ_RUNMODE=''|CQ_RUNMODE='author'|g"  > quickstart

EXPOSE 4502
ENTRYPOINT ["/AEM/aem/author/crx-quickstart/bin/quickstart","-D","FOREGROUND"]
