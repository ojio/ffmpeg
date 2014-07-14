FROM aquarius212/ffmpeg
MAINTAINER Michael Bishop <m@aquariusinteractive.com>

#RUN apt-get install -y -qq bison wget 
#RUN apt-get install -y -qq libcrypto++-dev libcrypto++-utils libcrypto++9 libssl-dev libpcre3-dev libpcre++-dev libpcre3 libpcrecpp0 libbz2-dev libcurl4-openssl-dev libxpm-dev libfreetype6-dev libfreetype6 t1lib-bin libt1-dev t1utils libmcrypt4 libmcrypt-dev libtomcrypt-dev libtomcrypt0 mcrypt libgmp-dev libgmp3-dev
RUN apt-get install -y -qq libenchant-dev libsqlite0-dev libenchant-dev libgd-dev libxpm4  icu-devtools libicu-dev libicu52 libedit-dev libedit2 libtidy-dev mysql-client apache2-dev apache2

RUN apt-mark hold php5

# PHP 5.3 Cannot find several multiarch headers/libraries
RUN ln -s /usr/lib/x86_64-linux-gnu/libXpm.so /usr/lib64/libXpm.so
RUN ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/include/gmp.h
RUN ldconfig

WORKDIR /tmp
RUN wget -q http://php.net/get/php-5.3.28.tar.bz2/from/this/mirror -O php-5.3.28.tar.bz2 && tar -xf php-5.3.28.tar.bz2

WORKDIR php-5.3.28

RUN CFLAGS="-g -O2 -fstack-protector --param=ssp-buffer-size=4 -Wformat -Wformat-security -fsigned-char -fno-strict-aliasing -gstabs -march=native -mtune=native" ./configure --build=x86_64-linux-gnu --host=x86_64-linux-gnu --program-prefix= --prefix=/usr --exec-prefix=/usr --bindir=/usr/bin --sbindir=/usr/sbin --sysconfdir=/etc --datadir=/usr/share --includedir=/usr/include --libdir=/usr/lib64 --libexecdir=/usr/libexec --localstatedir=/var --sharedstatedir=/var/lib --mandir=/usr/share/man --infodir=/usr/share/info --cache-file=../config.cache --with-libdir=lib64 --with-config-file-path=/etc/php5/apache2 --with-config-file-scan-dir=/etc/php5/apache2/conf.d --disable-debug --with-pic --disable-rpath --with-exec-dir=/usr/bin --with-png-dir=/usr --enable-gd-native-ttf --with-t1lib=/usr --without-gdbm --with-jpeg-dir=/usr --with-openssl --with-pcre-regex --with-zlib --with-layout=GNU --with-kerberos --with-libxml-dir=/usr  --with-mhash  --libdir=/usr/lib64/php --enable-pcntl  --enable-mbstring=shared --enable-mbregex --enable-calendar=shared --enable-bcmath=shared --with-bz2=static --enable-ctype=shared --enable-exif=shared --enable-ftp=shared --with-gettext=shared --with-iconv=shared --enable-sockets=shared --enable-tokenizer=shared --with-xmlrpc=shared  --enable-mysqlnd=shared --with-mysql=shared,mysqlnd --with-mysqli=shared,mysqlnd --with-mysql-sock=/var/lib/mysql/mysql.sock --enable-dom=shared  --enable-simplexml=shared --enable-xml  --enable-soap=shared --with-xsl=shared,/usr --enable-xmlreader=shared --enable-xmlwriter=shared --with-curl=static --enable-pdo=shared  --with-pdo-mysql=shared,mysqlnd  --without-readline --with-libedit --enable-phar=static --with-mcrypt=shared,/usr --with-tidy=shared,/usr  --enable-sysvmsg=static --enable-sysvshm=static --enable-sysvsem=static --enable-shmop=static --enable-posix=static  --enable-fileinfo=shared --enable-intl=shared --with-icu-dir=/usr --with-enchant=shared,/usr --with-pear --with-xpm-dir=/usr --with-gd --with-gmp=shared --with-libdir=lib64 --enable-session=static --enable-pdo=static --with-apxs2 --with-regex=php

RUN mkdir -p /etc/php5/apache2/
RUN make -j4 && make install
#RUN make clean

RUN pecl config-set php_ini /etc/php5/apache2/php.ini
RUN pear config-set php_ini /etc/php5/apache2/php.ini
RUN pear upgrade --force && pear install PHP_Archive-0.11.4

RUN pecl install -a memcache
RUN pecl install -a uploadprogress

ENV PHP_SERVER_INI /files/etc/php5/apache2/php.ini/PHP/

RUN CFLAGS="-g -O2 -fstack-protector --param=ssp-buffer-size=4 -Wformat -Wformat-security -fsigned-char -fno-strict-aliasing -gstabs -march=native -mtune=native" env


