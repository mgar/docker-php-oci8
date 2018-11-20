FROM php:7.2

LABEL maintainers="Miguel Ángel García <mgarcia.inf@gmail.com>"

RUN apt-get update
RUN apt-get install -y \
        apt-utils \
        libmcrypt-dev \
        libldb-dev \
        libldap2-dev \
        zlib1g-dev \  
        libicu-dev \
        openssl \
        libaio1 \
        ant \
        default-jdk \
        links \
        git \
        unzip \
        netcat

RUN ln -s /usr/lib/x86_64-linux-gnu/libldap.so /usr/lib/libldap.so && \
        ln -s /usr/lib/x86_64-linux-gnu/liblber.so /usr/lib/liblber.so

RUN docker-php-ext-install -j$(nproc) \
        mcrypt \
        zip \
        bcmath \ 
        ldap \
        intl

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

RUN apt-get install libaio-dev -y
RUN echo 'instantclient,/usr/local/instantclient' | pecl install oci8

ADD php/oci8.ini /usr/local/etc/php/conf.d/oci8.ini

RUN apt-get clean -y
