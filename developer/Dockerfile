FROM aquariusinteractive/base-ubuntu-204
MAINTAINER Aquarius Interactive <m@aquariusinteractive.com>

ENV DEBIAN_FRONTEND noninteractive
WORKDIR /tmp

RUN apt-get install -y cmake 

RUN wget http://www.cmake.org/files/v3.0/cmake-3.0.0.tar.gz
RUN tar -xvf cmake-3.0.0.tar.gz
WORKDIR cmake-3.0.0
RUN mkdir __build
WORKDIR __build
RUN cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr && make -j2 && cpack -G DEB
RUN apt-get -y remove 'cmake*'
RUN dpkg -i cmake*.deb
WORKDIR /tmp

RUN wget http://www.tortall.net/projects/yasm/releases/yasm-1.2.0.tar.gz
RUN tar -xvf yasm-1.2.0.tar.gz
WORKDIR yasm-1.2.0
RUN ./configure && make -j2 install
WORKDIR /tmp

