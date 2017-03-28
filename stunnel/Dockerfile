# stunnel Server
#
# VERSION 0.0.1

# Building from Ubuntu Precise
FROM ubuntu:latest

MAINTAINER Courtney Couch, courtney@moot.it

RUN apt-get update
RUN apt-get upgrade -y

RUN apt-get -y install build-essential wget curl
RUN apt-get -y install openssl libssl-dev

ENV STUNNEL_VERSION 4.56
RUN wget -O - ftp://ftp.stunnel.org/stunnel/archive/4.x/stunnel-$STUNNEL_VERSION.tar.gz | tar -C /usr/local/src -zxv

RUN mkdir -p /stunnel
VOLUME ["/stunnel"]

ADD stunnel.conf /stunnel/stunnel.conf

#Build stunnel
RUN cd /usr/local/src/stunnel-$STUNNEL_VERSION && ./configure && make && make install

EXPOSE 3306

CMD ["stunnel", "/stunnel/stunnel.conf"]
