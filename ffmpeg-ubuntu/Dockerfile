FROM ubuntu:14.04

MAINTAINER Michael Bishop <m@aquariusinteractive.com>
 
RUN apt-get update

RUN apt-get install -y subversion make cmake git gcc-4.8 gcc-4.8-doc gfortran-4.8 gfortran-4.8-doc cpp-4.8 cpp-4.8-doc  g++-4.8 yasm autoconf automake nasm libtool vim augeas-tools augeas-lenses augeas-doc curl software-properties-common python-software-properties bison wget re2c

RUN add-apt-repository "deb http://us.archive.ubuntu.com/ubuntu/ trusty universe multiverse" && add-apt-repository "deb http://us.archive.ubuntu.com/ubuntu/ trusty-updates universe multiverse"

RUN apt-get update &&  apt-get -y upgrade && apt-get -y dist-upgrade

RUN apt-get install -y yamdi libx264-dev x264 libgnutls-dev libass-dev libgstreamer-plugins-base1.0-0 libgstreamer-plugins-base1.0-dev libgstreamer-plugins-good1.0-0 libgstreamer-plugins-good1.0-dev libgstreamer1.0-0 libgstreamer1.0-dev libgstreamer-plugins-bad1.0-0 libgstreamer-plugins-bad1.0-dev libgstreamer-vaapi1.0-0 libgstreamer-vaapi1.0-dev libcrypto++-dev libcrypto++-utils libcrypto++9 libssl-dev libpcre3-dev libpcre++-dev libpcre3 libpcrecpp0 libbz2-dev libcurl4-openssl-dev libxpm-dev libfreetype6-dev libfreetype6 t1lib-bin libt1-dev t1utils libmcrypt4 libmcrypt-dev libtomcrypt-dev libtomcrypt0 mcrypt libxslt1.1 libxslt1-dev

RUN apt-get install -y libvpx-dev vpx-tools libfaad-dev libfaac-dev libopus-dev opus-tools libjpeg-turbo8 libjpeg-turbo8-dev libjpeg-turbo-progs libturbojpeg libopenjpeg2 libopenjpeg-dev openjpeg-tools libmpeg2-4-dev libmpeg2-4 mp4v2-utils libmp4v2-2 libmp4v2-dev libwebp-dev libwebp5 libwebpdemux1 libwebpmux1 libgsm1-dev libgsmme-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libopencore-amrnb0 libopencore-amrwb0 libpulse-dev librtmp-dev libschroedinger-1.0-0 libschroedinger-dev libspeex-dev libspeex1 libspeexdsp-dev libspeexdsp1 libtheora-dev libtwolame-dev libvo-aacenc-dev libvo-amrwbenc-dev libvorbis-dev libxvidcore-dev  libfdk-aac-dev libfdk-aac0 libfaad2 libfaad-dev faad

#ffmpeg
WORKDIR /tmp
RUN git clone --depth 1 git://source.ffmpeg.org/ffmpeg
WORKDIR ffmpeg
RUN ./configure --shlibdir=/usr/lib64 --prefix=/usr --mandir=/usr/share/man --libdir=/usr/lib64 --enable-static --extra-cflags='-fmessage-length=0 -grecord-gcc-switches -fstack-protector -O2 -Wall -D_FORTIFY_SOURCE=2 -funwind-tables -fasynchronous-unwind-tables -g -fPIC -I/usr/include/gsm' --enable-gpl --disable-x11grab --enable-version3 --enable-pthreads --enable-avfilter --enable-libpulse --enable-libvpx --enable-libopus --enable-libass --disable-libx265 --enable-libmp3lame --enable-libvorbis --enable-libtheora --enable-libspeex --enable-libxvid --enable-libx264 --enable-libschroedinger --enable-libgsm --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-postproc --disable-libdc1394 --enable-librtmp --enable-libfreetype --enable-avresample --enable-libtwolame --enable-libvo-aacenc --enable-gnutls --enable-nonfree --enable-libfdk-aac --enable-libfaac --enable-libopenjpeg --enable-gray --enable-libwebp && make -j4 install && make install-data && make clean

WORKDIR tools
RUN gcc qt-faststart.c -o qt-faststart && mv qt-faststart /usr/local/bin


#mplayer / mencoder
WORKDIR /tmp
RUN svn checkout svn://svn.mplayerhq.hu/mplayer/trunk mplayer
WORKDIR mplayer
RUN ./configure && make -j2 install && make clean

WORKDIR /tmp

