FROM centos/php-71-centos7:latest

LABEL maintainers="Miguel Ángel García <mgarcia.inf@gmail.com>"

USER root

RUN yum -y update && yum -y install epel-release

RUN yum install -y libmcrypt \
        libldb-devel \
        openssl \
        git \
        zip \
        vim \
        ant \
        libaio \
        unzip \
        netcat \
        sudo

RUN yum -y install rh-php71-php-devel \
        sclo-php71-php-mcrypt \
        rh-php71-php-zip \
        rh-php71-php-bcmath \
        rh-php71-php-ldap \
        rh-php71-php-intl


RUN ln -s /usr/lib/x86_64-linux-gnu/libldap.so /usr/lib/libldap.so && \
        ln -s /usr/lib/x86_64-linux-gnu/liblber.so /usr/lib/liblber.so && \
        ln -s /opt/rh/rh-php71/root/usr/bin/php /usr/local/bin/php

# Oracle instantclient
ADD oracle/instantclient-basic-linux.x64-11.2.0.4.0.zip /tmp/instantclient-basic-linux.x64-11.2.0.4.0.zip
ADD oracle/instantclient-sdk-linux.x64-11.2.0.4.0.zip /tmp/instantclient-sdk-linux.x64-11.2.0.4.0.zip
ADD oracle/instantclient-sqlplus-linux.x64-11.2.0.4.0.zip /tmp/instantclient-sqlplus-linux.x64-11.2.0.4.0.zip

RUN unzip /tmp/instantclient-basic-linux.x64-11.2.0.4.0.zip -d /usr/local/
RUN unzip /tmp/instantclient-sdk-linux.x64-11.2.0.4.0.zip -d /usr/local/
RUN unzip /tmp/instantclient-sqlplus-linux.x64-11.2.0.4.0.zip -d /usr/local/

RUN ln -s /usr/local/instantclient_11_2 /usr/local/instantclient
RUN ln -s /usr/local/instantclient/libclntsh.so.11.1 /usr/local/instantclient/libclntsh.so
RUN ln -s /usr/local/instantclient/sqlplus /usr/bin/sqlplus


RUN echo 'instantclient,/usr/local/instantclient' | pecl install oci8
ADD php/oci8.ini /etc/opt/rh/rh-php71/php.d/oci8.ini

RUN yum install libaio-devel -y
RUN yum clean all && rm -rf /var/cache/yum
