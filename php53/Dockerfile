FROM aquarius212/ffmpeg
MAINTAINER Michael Bishop <m@aquariusinteractive.com>

RUN apt-get install -y bison wget
RUN apt-get install -y libcrypto++-dev libcrypto++-utils libcrypto++9 libssl-dev libpcre3-dev libpcre++-dev libpcre3 libpcrecpp0
RUN apt-mark hold php5

WORKDIR /tmp
RUN wget -q http://php.net/get/php-5.3.28.tar.bz2/from/this/mirror -O php-5.3.28.tar.bz2 && tar -xf php-5.3.28.tar.bz2

WORKDIR php-5.3.28

./configure --program-prefix= --prefix=/usr --exec-prefix=/usr --bindir=/usr/bin --sbindir=/usr/sbin --sysconfdir=/etc --datadir=/usr/share --includedir=/usr/include --libdir=/usr/lib64 --libexecdir=/usr/libexec --localstatedir=/var --sharedstatedir=/var/lib --mandir=/usr/share/man --infodir=/usr/share/info --cache-file=../config.cache --with-libdir=lib64 --with-config-file-path=/etc --with-config-file-scan-dir=/etc/php.d --disable-debug --with-pic --disable-rpath --with-exec-dir=/usr/bin --with-freetype-dir=/usr --with-png-dir=/usr --with-xpm-dir=/usr --enable-gd-native-ttf --with-t1lib=/usr --without-gdbm --with-jpeg-dir=/usr --with-openssl --with-pcre-regex=/usr --with-zlib --with-layout=GNU --with-kerberos --with-libxml-dir=/usr  --with-mhash  --libdir=/usr/lib64/php --enable-pcntl  --with-imap=shared --with-imap-ssl --enable-mbstring=shared --enable-mbregex --with-gd=shared,/usr --with-gmp=shared --enable-calendar=shared --enable-bcmath=shared --with-bz2=shared --enable-ctype=shared --enable-exif=shared --enable-ftp=shared --with-gettext=shared --with-iconv=shared --enable-sockets=shared --enable-tokenizer=shared --with-xmlrpc=shared  --enable-mysqlnd=shared --with-mysql=shared,mysqlnd --with-mysqli=shared,mysqlnd --with-mysql-sock=/var/lib/mysql/mysql.sock --enable-dom=shared  --enable-simplexml=shared --enable-xml  --enable-soap=shared --with-xsl=shared,/usr --enable-xmlreader=shared --enable-xmlwriter=shared --with-curl=shared,/usr --enable-pdo=shared  --with-pdo-mysql=shared,mysqlnd  --without-readline --with-libedit --enable-phar=shared --with-mcrypt=shared,/usr --with-tidy=shared,/usr  --enable-sysvmsg=shared --enable-sysvshm=shared --enable-sysvsem=shared --enable-shmop=shared --enable-posix=shared  --enable-fileinfo=shared --enable-intl=shared --with-icu-dir=/usr --with-enchant=shared,/usr --enable-fpm --with-fpm-user=www-data --with-fpm-group=www-data --with-pear --without-pdo-sqlite --without-sqlite3 --without-sqlite

