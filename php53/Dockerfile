FROM aquarius212/ffmpeg
MAINTAINER Michael Bishop <m@aquariusinteractive.com>

RUN apt-get install -y bison wget
RUN apt-mark hold php5

WORKDIR /tmp
RUN wget http://php.net/get/php-5.3.28.tar.bz2/from/this/mirror -O php-5.3.28.tar.bz2 && tar -xvf php-5.3.28.tar.bz2

WORKDIR php-5.3.28


