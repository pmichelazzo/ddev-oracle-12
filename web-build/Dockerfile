
# You can copy this Dockerfile.example to Dockerfile to add configuration
# or packages or anything else to your webimage
ARG BASE_IMAGE=drud/ddev-webserver:v1.12.1
FROM $BASE_IMAGE

# Oracle instantclient
ADD oracle/instantclient-basic-linux.x64-12.1.0.2.0.zip /tmp/instantclient-basic-linux.x64-12.1.0.2.0.zip
ADD oracle/instantclient-sdk-linux.x64-12.1.0.2.0.zip /tmp/instantclient-sdk-linux.x64-12.1.0.2.0.zip
ADD oracle/instantclient-sqlplus-linux.x64-12.1.0.2.0.zip /tmp/instantclient-sqlplus-linux.x64-12.1.0.2.0.zip

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y -o Dpkg::Options::="--force-confnew" --no-install-recommends --no-install-suggests gcc make autoconf libc-dev pkg-config php-pear php7.3-dev libmcrypt-dev build-essential libaio1 unzip

RUN unzip /tmp/instantclient-basic-linux.x64-12.1.0.2.0.zip -d /usr/local/
RUN unzip /tmp/instantclient-sdk-linux.x64-12.1.0.2.0.zip -d /usr/local/
RUN unzip /tmp/instantclient-sqlplus-linux.x64-12.1.0.2.0.zip -d /usr/local/
RUN ln -s /usr/local/instantclient_12_1 /usr/local/instantclient
RUN ln -s /usr/local/instantclient/libclntsh.so.12.1 /usr/local/instantclient/libclntsh.so
RUN ln -s /usr/local/instantclient/sqlplus /usr/bin/sqlplus

RUN echo '/usr/local/instantclient'  > /etc/ld.so.conf.d/oracle-instantclient
RUN echo '/usr/local/instantclient' >> /etc/ld.so.conf.d/x86_64-linux-gnu.conf

RUN ldconfig


RUN apt-get install libaio-dev -y

RUN echo 'instantclient,/usr/local/instantclient' | pecl install oci8

RUN apt-get clean -y


# see more https://gist.github.com/hewerthomn/81eea2935051eb2500941a9309bca703
# https://github.com/FabriZZio/docker-php-oci8/blob/master/Dockerfile
