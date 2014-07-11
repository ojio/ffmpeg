FROM ubuntu:12.04
MAINTAINER Aquarius Interactive <m@aquariusinteractive.com>

ENV DEBIAN_FRONTEND noninteractive
WORKDIR /tmp

RUN sed -i "/^# deb .*partner/ s/^# //" /etc/apt/sources.list
RUN echo "deb http://archive.ubuntu.com/ubuntu/ precise multiverse" >> /etc/apt/sources.list
RUN apt-get -y install software-properties-common wget python-software-properties pkg-config
RUN add-apt-repository -y ppa:ubuntu-toolchain-r/test
RUN apt-get update
RUN apt-get -y install htop bison re2c make binutils vim sudo man rubygems  python-pip

RUN wget http://archive.getdeb.net/install_deb/getdeb-repository_0.1-1~getdeb1_all.deb
RUN dpkg -i getdeb-repository_0.1-1~getdeb1_all.deb
RUN rm -f /tmp/getdeb-repository_0.1-1~getdeb1_all.deb
RUN add-apt-repository -y ppa:videolan/stable-daily
RUN sudo add-apt-repository -y ppa:webupd8team/y-ppa-manager

RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get -y dist-upgrade

ENV DEBIAN_FRONTEND dialog
