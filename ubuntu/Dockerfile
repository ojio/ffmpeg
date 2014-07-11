FROM aquarius212/dev-ubuntu-204
MAINTAINER Aquarius Interactive <m@aquariusinteractive.com>

ENV DEBIAN_FRONTEND noninteractive
WORKDIR /tmp

RUN apt-get -y install imagemagick libmagickcore4-extra libmagickwand4 libwebp2 webp

RUN gem install flvtool2

#MYSql
RUN apt-get -y install mysql-server
RUN sed -i -e "s/^bind-address\s*=\s*127.0.0.1/bind-address = 0.0.0.0/" /etc/mysql/my.cnf
RUN sed -i -e "s/^datadir\s*=\s*\/var\/lib\/mysql/datadir=\/mysql/" /etc/mysql/my.cnf

#PHP
RUN apt-get -y install php5-cli php5-curl php5-fpm php5-gd php5-imagick php5-mcrypt php5-memcache php5-mysqlnd php5-tidy php-pear nginx-extras
RUN sed -i -e "s/listen = 127.0.0.1:9000/listen=\/var\/run\/php5-fpm.sock/" /etc/php5/fpm/pool.d/www.conf
RUN sed -i -e "s/;listen.owner = www-data/listen.owner = www-data/" /etc/php5/fpm/pool.d/www.conf
RUN sed -i -e "s/;listen.group = www-data/listen.group = www-data/" /etc/php5/fpm/pool.d/www.conf
RUN sed -i -e "s/;listen.mode = 0660/listen.mode = 0660/" /etc/php5/fpm/pool.d/www.conf

#PHP
RUN sed -i -e "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g" /etc/php5/fpm/php.ini
RUN sed -i -e "s/output_buffering = 4096/output_buffering = Off/g" /etc/php5/fpm/php.ini
RUN sed -i -e "s/register_argc_argv = Off/register_argc_argv = On/g" /etc/php5/fpm/php.ini
RUN sed -i -e "s/upload_max_filesize = 2M/upload_max_filesize = 500M/g" /etc/php5/fpm/php.ini
RUN sed -i -e "s/post_max_size = 8M/post_max_size = 500M/g" /etc/php5/fpm/php.ini
RUN sed -i -e "s/max_execution_time = 30/max_execution_time = 1800/g" /etc/php5/fpm/php.ini
RUN sed -i -e "s/max_input_time = 60/max_input_time = 1800/g" /etc/php5/fpm/php.ini
RUN sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php5/fpm/php-fpm.conf
RUN sed -i -e "s/;catch_workers_output\s*=\s*yes/catch_workers_output = yes/g" /etc/php5/fpm/pool.d/www.conf

ADD ioncube_loader_lin_5.3.so /usr/lib/php5/20090626/
RUN echo "zend_extension = /usr/lib/php5/20090626/ioncube_loader_lin_5.3.so" > /etc/php5/fpm/conf.d/20-ioncube.ini


#NGINX
#ADD default.nginx.conf /tmp/default.nginx.conf
#RUN rm -f /etc/nginx/sites-available/default
#RUN rm -f /etc/nginx/sites-enabled/default
#RUN mv -f /tmp/default.nginx.conf /etc/nginx/sites-enabled/default
#RUN echo "daemon off;" >> /etc/nginx/nginx.conf
#RUN sed -i -e "s/server_name localhost;server_name name_here/g" /etc/nginx/sites-available/default

#SUPERVISORD
RUN easy_install supervisor
RUN easy_install supervisor-stdout
RUN mkdir /var/log/supervisor
ADD supervisord.conf /etc/supervisord.conf

WORKDIR /tmp
RUN apt-get install -y libass4 libenca-dev libfontconfig1-dev libfribidi-dev libgpac1 libogg-dev checkinstall libass-dev libass4 libenca-dev libfaac-dev libfontconfig1-dev libfribidi-dev libgpac-dev libgpac1 libmp3lame-dev libogg-dev libopencore-amrnb-dev
RUN apt-get install -y libopencore-amrwb-dev libtheora-dev libvorbis-dev texi2html

#x264
RUN git clone --depth 1 git://git.videolan.org/x264
WORKDIR x264
RUN ./configure --enable-static --enable-shared && make -j2
RUN checkinstall --pkgname=x264 --pkgversion="3:$(./version.sh |  awk -F'[" ]' '/POINT/{print $4"+git"$5}')" --backup=no --deldoc=yes  --fstrans=no --default

#fdk-aac
WORKDIR /tmp
RUN git clone --depth 1 git://github.com/mstorsjo/fdk-aac.git
WORKDIR fdk-aac
RUN autoreconf -fiv && ./configure --disable-shared && make -j2
RUN checkinstall --pkgname=fdk-aac --pkgversion="$(date +%Y%m%d%H%M)-git" --backup=no  --deldoc=yes --fstrans=no --default

#libvpx
WORKDIR /tmp
RUN git clone -q --depth 1 https://chromium.googlesource.com/webm/libvpx
WORKDIR libvpx
RUN ./configure --disable-examples --disable-unit-tests && make -j2
RUN checkinstall --pkgname=libvpx --pkgversion="1:$(date +%Y%m%d%H%M)-git" --backup=no  --deldoc=yes --fstrans=no --default

#opus
WORKDIR /tmp
RUN git clone --depth 1 git://git.xiph.org/opus.git
WORKDIR opus
RUN ./autogen.sh && ./configure --disable-shared && make -j2
RUN checkinstall --pkgname=libopus --pkgversion="$(date +%Y%m%d%H%M)-git" --backup=no  --deldoc=yes --fstrans=no --default
RUN ldconfig

#ffmpeg
WORKDIR /tmp
RUN git clone --depth 1 git://source.ffmpeg.org/ffmpeg
WORKDIR ffmpeg
RUN ./configure --enable-gpl --enable-libass --enable-libfaac --enable-libfdk-aac --enable-libmp3lame --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-librtmp --enable-libtheora  --enable-libvorbis --enable-libvpx --enable-libx264 --enable-nonfree --enable-version3
RUN make -j2 && sudo checkinstall --pkgname=ffmpeg --pkgversion="7:$(date +%Y%m%d%H%M)-git" --backup=no  --deldoc=yes --fstrans=no --default
RUN hash -r

#RUN apt-get -f install
#RUN apt-get -y autoremove
#RUN apt-get -y autoclean
#RUN apt-get -y clean

EXPOSE 80
ENV DEBIAN_FRONTEND dialog
CMD ["/usr/local/bin/supervisord"]
