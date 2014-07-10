FROM ubuntu:12.04
MAINTAINER Aquarius Interactive <m@aquariusinteractive.com>

ENV DEBIAN_FRONTEND noninteractive
WORKDIR /tmp

RUN sed -i "/^# deb .*partner/ s/^# //" /etc/apt/sources.list
RUN echo "deb http://archive.ubuntu.com/ubuntu/ precise multiverse" >> /etc/apt/sources.list
RUN apt-get update
RUN apt-get -y install python-software-properties software-properties-common wget htop gcc bison re2c make binutils pkg-config vim sudo man rubygems  python-pip

RUN wget http://archive.getdeb.net/install_deb/getdeb-repository_0.1-1~getdeb1_all.deb
RUN dpkg -i getdeb-repository_0.1-1~getdeb1_all.deb
RUN rm -f /tmp/getdeb-repository_0.1-1~getdeb1_all.deb
RUN add-apt-repository -y ppa:videolan/stable-daily
RUN sudo add-apt-repository -y ppa:webupd8team/y-ppa-manager

RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get -y dist-upgrade

RUN apt-get -y install libavcodec-extra-53 libavformat-extra-53 libavutil-extra-51 libpostproc-extra-52 libswscale-extra-2 libtheora0 libvorbis0a libvorbisenc2 libvorbisfile3
RUN apt-get -y install libvpx1 libxvidcore4 vpx-tools mencoder faad sox libpostproc-extra-52 libswscale-extra-2 libcharls1 libjasper1 libjpeg-turbo8 libjpeg62 libjpeg8 libopenjpeg2 libturbojpeg 
RUN apt-get -y install ffmpeg gstreamer0.10-ffmpeg libxine1-ffmpeg libxine2-ffmpeg libvisual-0.4-plugins libglide3 faac libfaac0 ffmpeg2theora alac-decoder flac yamdi
RUN apt-get -y install imagemagick libmagickcore4-extra libmagickwand4 libwebp2 webp unzip 

#RUN yum -y install libwebp-tools gstreamer-plugins-good gstreamer-plugins-bad gstreamer-plugins-ugly gstreamer gstreamer-rtsp gstreamer-ffmpeg gstreamer-tools
#RUN yum -y install ffmpeg ffmpeg-libs ImageMagick mencoder oggconvert oggvideotools ogmtools gd-progs

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

RUN apt-get -f install
RUN apt-get autoremove
RUN apt-get -y autoclean
RUN apt-get -y clean

#PHP
ADD ioncube_loader_lin_5.3.so /usr/lib/php5/20090626/
RUN sed -i -e "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g" /etc/php5/fpm/php.ini
RUN sed -i -e "s/output_buffering = 4096/output_buffering = Off/g" /etc/php5/fpm/php.ini
RUN sed -i -e "s/register_argc_argv = Off/register_argc_argv = On/g" /etc/php5/fpm/php.ini
RUN sed -i -e "s/upload_max_filesize = 2M/upload_max_filesize = 500M/g" /etc/php5/fpm/php.ini
RUN sed -i -e "s/post_max_size = 8M/post_max_size = 500M/g" /etc/php5/fpm/php.ini
RUN sed -i -e "s/max_execution_time = 30/max_execution_time = 1800/g" /etc/php5/fpm/php.ini
RUN sed -i -e "s/max_input_time = 60/max_input_time = 1800/g" /etc/php5/fpm/php.ini
RUN sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php5/fpm/php-fpm.conf
RUN sed -i -e "s/;catch_workers_output\s*=\s*yes/catch_workers_output = yes/g" /etc/php5/fpm/pool.d/www.conf
RUN echo "zend_extension = /usr/lib/php5/20090626/ioncube_loader_lin_5.3.so" > /etc/php5/fpm/conf.d/20-ioncube.ini

#NGINX
ADD default.nginx.conf /tmp/default.nginx.conf
#RUN rm -f /etc/nginx/sites-available/default
#RUN rm -f /etc/nginx/sites-enabled/default
RUN mv -f /tmp/default.nginx.conf /etc/nginx/sites-enabled/default
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
#RUN mkdir -p /wwwroot/default
#RUN chown www-data:www-data /wwwroot -R
#RUN sed -i -e "s/server_name localhost;server_name name_here/g" /etc/nginx/sites-available/default

#SUPERVISORD
RUN easy_install supervisor
RUN easy_install supervisor-stdout
RUN mkdir /var/log/supervisor
ADD supervisord.conf /etc/supervisord.conf

EXPOSE 80
ENV DEBIAN_FRONTEND dialog
CMD ["/usr/local/bin/supervisord"]
