FROM centos:latest

RUN yum install httpd -y
RUN yum install policycoreutils -y
RUN yum install initscripts -y
RUN yum install wget -y

WORKDIR /
RUN mkdir /opt/www
RUN mkdir /opt/www/conf
RUN mkdir /opt/www/modules
RUN mkdir /opt/www/installer

WORKDIR /opt/www/installer
RUN wget https://www.adobeaemcloud.com/content/companies/public/adobe/dispatcher/dispatcher/_jcr_content/top/download_8/file.res/dispatcher-apache2.4-linux-x86-64-4.2.2.tar.gz
RUN tar -xvf dispatcher-apache2.4-linux-x86-64-4.2.2.tar.gz
RUN rm dispatcher-apache2.4-linux-x86-64-4.2.2.tar.gz
RUN cp dispatcher-apache2.4-4.2.2.so /opt/www/modules

WORKDIR /opt/www/modules
RUN ln -s dispatcher-apache2.4-4.2.2.so mod_dispatcher.so

COPY dispatcher.any /opt/www/conf/dispatcher.any
COPY httpd.conf /etc/httpd/conf/httpd.conf
COPY cq.conf /etc/httpd/conf.d/cq.conf
EXPOSE 80
ENTRYPOINT ["/usr/sbin/httpd", "-D", "FOREGROUND"]
