FROM mmckeen/opensuse-13-1
MAINTAINER Aquarius Interactive <m@aquariusinteractive.comt>

RUN zypper ar -f -n packman-essentials http://packman.inode.at/suse/openSUSE_13.1/Essentials/ packman-essentials
RUN zypper ar -f -n packman-multimedia http://packman.inode.at/suse/openSUSE_13.1/Multimedia/ packman-multimedia
RUN zypper ar  http://download.opensuse.org/repositories/Apache:/Modules/Apache_openSUSE_13.1/Apache:Modules.repo
RUN zypper ar  http://download.opensuse.org/repositories/security/openSUSE_13.1/security.repo
#RUN zypper ar  http://download.opensuse.org/repositories/server:/php:/extensions/openSUSE_13.1/server:php:extensions.repo
#RUN zypper ar  http://download.opensuse.org/repositories/server:/php:/applications/openSUSE_13.1/server:php:applications.repo
RUN zypper ar -n php53 http://download.opensuse.org/repositories/home:/weberho:/PHP53/openSUSE_13.1/home:weberho:PHP53.repo

RUN zypper -n --gpg-auto-import-keys ref && zypper refresh -s -f && zypper -n up

RUN zypper -n install yamdi libx264-devel x264 gstreamer-0_10-plugins-bad gstreamer-0_10-plugins-ugly gstreamer-0_10-plugins-ugly-orig-addon gstreamer-0_10-plugins-ffmpeg gnutls gnutls-devel libass-devel 

# Developer tools
RUN zypper -n install subversion make cmake git gcc gcc-fortran gcc-c++ yasm autoconf automake nasm libtool vim augeas curl

# Libraries and source for compilation and various runtime libs
RUN zypper -n install libvpx-devel vpx-tools libfaad-devel libfaac-devel libopus-devel opus-tools libjpeg-turbo libjpeg8 libjpeg8-devel openjpeg openjpeg-devel libmpeg2-devel mp4v2 libmp4v2-2 libmp4v2-devel mp4als libwebp-devel libwebpdemux0 libwebpmux0 libgsm-devel libmp3lame-devel libopencore-amr-devel libpulse-devel librtmp-devel schroedinger-devel libspeex libspeexdsp1 speex-devel libtheora-devel libtwolame-devel libvo-aacenc-devel libvo-amrwbenc-devel libvorbis-devel libxvidcore-devel 

#fdk-aac
WORKDIR /tmp
RUN git clone --depth 1 git://git.code.sf.net/p/opencore-amr/fdk-aac
WORKDIR fdk-aac
RUN autoreconf -fiv && ./configure --prefix=/usr --enable-static --enable-shared --libdir=/usr/lib64 --with-pic && make -j4 install

#ffmpeg
WORKDIR /tmp
RUN git clone --depth 1 git://source.ffmpeg.org/ffmpeg
WORKDIR ffmpeg
RUN ./configure --shlibdir=/usr/lib64 --prefix=/usr --mandir=/usr/share/man --libdir=/usr/lib64 --enable-static --extra-cflags='-fmessage-length=0 -grecord-gcc-switches -fstack-protector -O2 -Wall -D_FORTIFY_SOURCE=2 -funwind-tables -fasynchronous-unwind-tables -g -fPIC -I/usr/include/gsm' --enable-gpl --disable-x11grab --enable-version3 --enable-pthreads --enable-avfilter --enable-libpulse --enable-libvpx --enable-libopus --enable-libass --disable-libx265 --enable-libmp3lame --enable-libvorbis --enable-libtheora --enable-libspeex --enable-libxvid --enable-libx264 --enable-libschroedinger --enable-libgsm --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-postproc --disable-libdc1394 --enable-librtmp --enable-libfreetype --enable-avresample --enable-libtwolame --enable-libvo-aacenc --enable-gnutls --enable-nonfree --enable-libfdk-aac --enable-libfaac --enable-libopenjpeg --enable-gray --enable-opengl --enable-libwebp && make -j4 install && make install-data
WORKDIR tools
RUN gcc qt-faststart.c -o qt-faststart && mv qt-faststart /usr/local/bin

#mplayer / mencoder
WORKDIR /tmp
RUN svn checkout svn://svn.mplayerhq.hu/mplayer/trunk mplayer
WORKDIR mplayer
RUN ./configure && make -j2 install

WORKDIR /tmp

#PHP
ENV PHP_VERSION 5.3
ENV PHP_LONG_VER 5.3.28-3.1
RUN zypper -n install php5=${PHP_LONG_VER} php-fpm=${PHP_LONG_VER} php5-zlib=${PHP_LONG_VER} php5-zip=${PHP_LONG_VER} php5-sysvmsg=${PHP_LONG_VER} php5-sysvsem=${PHP_LONG_VER} php5-readline=${PHP_LONG_VER} imagemagick imagemagick-devel
RUN zypper -n install php5-posix=${PHP_LONG_VER} php5-bcmath=${PHP_LONG_VER} php5-bz2=${PHP_LONG_VER} php5-calendar=${PHP_LONG_VER} php5-curl=${PHP_LONG_VER} php5-devel=${PHP_LONG_VER} php5-mcrypt=${PHP_LONG_VER} php5-xml*=${PHP_LONG_VER} php5-gd=${PHP_LONG_VER} php5-gettext=${PHP_LONG_VER} php5-mbstring=${PHP_LONG_VER} php5-mysql=${PHP_LONG_VER} php5-pear=${PHP_LONG_VER} php5-fileinfo=${PHP_LONG_VER} php5-imagick apache2-mod_php5=${PHP_LONG_VER}
#RUN zypper -n install php5 php5-zlib php5-zip php5-sysvshm php5-sysvmsg php5-sysvsem php5-posix php5-readline php5-bcmath php5-bz2 php5-calendar php5-curl php5-devel php5-mcrypt php5-ctype php5-dom php5-iconv php5-json php5-sqlite php5-tokenizer php5-xmlreader php5-xmlwriter php5-gd php5-gettext php5-mbstring php5-mysql php5-pear php5-fileinfo php5-imagick

RUN mv /etc/php5/fpm/php-fpm.conf.default /etc/php5/fpm/php-fpm.conf

RUN cd `pear config-get php_dir` && mv .channels .channels-broken && pear update-channels
RUN cd `pecl config-get php_dir` && mv .channels .channels-broken && pecl update-channels

#ioncube
ADD http://downloads3.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.bz2 /tmp/
RUN tar -xvf ioncube_loaders_lin_x86-64.tar.bz2

WORKDIR ioncube
RUN cp ioncube_loader_lin_${PHP_VERSION}.so `php-config --extension-dir`
RUN echo zend_extension=`php-config --extension-dir`/ioncube_loader_lin_${PHP_VERSION}.so > /etc/php5/conf.d/ioncube.ini

WORKDIR /tmp
RUN rm -rf *

#Apache
RUN echo "/usr/sbin/suexec2                                       root:root         0755" >> /etc/permissions
RUN zypper -n install apache2-event apache2-mod_fcgid apache2-utils w3m
RUN touch /etc/apache2/sysconfig.d/include.conf

# Setup the apache config files
#RUN /usr/sbin/rcapache2 start && /usr/sbin/rcapache2 stop

RUN pear upgrade --force
RUN pecl config-set php_ini /etc/php5/fpm/php.ini
RUN pear config-set php_ini /etc/php5/fpm/php.ini
RUN pecl install -a memcache
RUN pecl install -a uploadprogress

ENV PHP_SERVER_INI /files/etc/php5/fpm/php.ini/PHP/
RUN augtool touch ${PHP_SERVER_INI}/magic_quotes_gpc
RUN augtool set ${PHP_SERVER_INI}/magic_quotes_gpc 1
RUN augtool set ${PHP_SERVER_INI}/upload_max_filesize 500M
RUN augtool set ${PHP_SERVER_INI}/post_max_size 500M
RUN augtool set ${PHP_SERVER_INI}/max_execution_time 7200
RUN augtool set ${PHP_SERVER_INI}/max_input_time 7200
RUN augtool set ${PHP_SERVER_INI}/memory_limit 640M
RUN augtool set ${PHP_SERVER_INI}/expose_php off
RUN augtool set /files/etc/php5/cli/php.ini/PHP/register_argc_argv on
RUN sed -i "s/;error_log = log\/php-fpm.log/error_log=syslog/" /etc/php5/fpm/php-fpm.conf

RUN zypper -n install memcached 
RUN zypper -n rm git-web

RUN chkstat --set --system

EXPOSE 80
EXPOSE 443

VOLUME ["/srv/www/htdocs"]

CMD apache2ctl -D FOREGROUND

