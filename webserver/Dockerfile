#FROM fedora:20
FROM aquariusinteractive/fedora20
MAINTAINER Aquarius Interactive <m@aquariusinteractive.com>

WORKDIR /tmp
ENV CFLAGS -O2 -march=native -mtune=native -lssl -lcrypto
ENV CXXFLAGS -O2 -march=native -mtune=native -lssl -lcrypto

RUN echo "exclude=php*" >> /etc/yum.conf

RUN yum -y install drpmsync deltarpm tree

RUN yum -y install gcc gcc-c++ bison re2c libxml2-devel make binutils libscrypt mhash sha zlib-devel zlib zopfli autoconf wget bzip2 gem file 
RUN yum -y install memcached
RUN yum -y install libogg-devel libwebp-devel t1lib-devel libc-client-devel
RUN yum -y install libcurl-devel openssl-devel openssl-libs ffmpeg-devel bzip2-devel gmp-devel libedit-devel libicu-devel freetds-devel
RUN yum -y install libexif-devel gd-devel mhash-devel libmcrypt libmcrypt-devel sendmail-devel faac-devel libtidy-devel enchant-devel libxslt-devel
RUN yum -y install ImageMagick-devel 
RUN yum -y install memcached-devel libmemcached-devel mm-devel libtool-ltdl-devel 

RUN yum -y update
RUN yum clean all

# Install PHP
ADD php-5.3.28.tar.bz2 /tmp
WORKDIR php-5.3.28
ENV LDLIBS -lssl -lcrypto
ENV LFLAGS -L/usr/local/lib

RUN ./configure --build=x86_64-redhat-linux-gnu --host=x86_64-redhat-linux-gnu --program-prefix= --prefix=/usr --exec-prefix=/usr --bindir=/usr/bin --sbindir=/usr/sbin --sysconfdir=/etc --datadir=/usr/share --includedir=/usr/include --libdir=/usr/lib64 --libexecdir=/usr/libexec --localstatedir=/var --sharedstatedir=/var/lib --mandir=/usr/share/man --infodir=/usr/share/info --cache-file=../config.cache --with-libdir=lib64 --with-config-file-path=/etc --with-config-file-scan-dir=/etc/php.d --disable-debug --with-pic --disable-rpath --with-exec-dir=/usr/bin --with-freetype-dir=/usr --with-png-dir=/usr --with-xpm-dir=/usr --enable-gd-native-ttf --with-t1lib=/usr --without-gdbm --with-jpeg-dir=/usr --with-openssl --with-pcre-regex=/usr --with-zlib --with-layout=GNU --with-kerberos --with-libxml-dir=/usr  --with-mhash  --libdir=/usr/lib64/php --enable-pcntl  --with-imap=shared --with-imap-ssl --enable-mbstring=shared --enable-mbregex --with-gd=shared,/usr --with-gmp=shared --enable-calendar=shared --enable-bcmath=shared --with-bz2=shared --enable-ctype=shared --enable-exif=shared --enable-ftp=shared --with-gettext=shared --with-iconv=shared --enable-sockets=shared --enable-tokenizer=shared --with-xmlrpc=shared  --enable-mysqlnd=shared --with-mysql=shared,mysqlnd --with-mysqli=shared,mysqlnd --with-mysql-sock=/var/lib/mysql/mysql.sock --enable-dom=shared  --enable-simplexml=shared --enable-xml  --enable-soap=shared --with-xsl=shared,/usr --enable-xmlreader=shared --enable-xmlwriter=shared --with-curl=shared,/usr --enable-pdo=shared  --with-pdo-mysql=shared,mysqlnd  --without-readline --with-libedit --enable-phar=shared --with-mcrypt=shared,/usr --with-tidy=shared,/usr  --enable-sysvmsg=shared --enable-sysvshm=shared --enable-sysvsem=shared --enable-shmop=shared --enable-posix=shared  --enable-fileinfo=shared --enable-intl=shared --with-icu-dir=/usr --with-enchant=shared,/usr --enable-fpm --with-fpm-user=www-data --with-fpm-group=www-data --with-pear --without-pdo-sqlite --without-sqlite3 --without-sqlite
RUN make -j2
RUN make install
RUN mkdir /etc/php.d

RUN pear upgrade --force
RUN pear install PHP_Archive-0.11.4
RUN printf "\n" | pecl install -a memcache
RUN ls /usr/lib64/php/20090626/*.so -1 | xargs -L1 -n1 basename |  xargs -n1 -I {} printf "extension=%s\n" {} >> /etc/php.d/extensions.ini

WORKDIR /tmp
#RUN rm -rf *


