Apache+PHP build pack
========================

This is a build pack bundling PHP and Apache for Heroku apps.

Configuration
-------------

The config files are bundled with the LP itself:

* conf/httpd.conf
* conf/php.ini


Pre-compiling binaries
----------------------

Fix mountain lion: sudo ln -s /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain /Applications/Xcode.app/Contents/Developer/Toolchains/OSX10.8.xctoolchain
Install PCRE: brew install pcre

    # apache
    mkdir /app //temprarily sudo it to 777
    curl http://apache.cyberuse.com/httpd/httpd-2.4.2.tar.gz -O
    tar xvzf httpd-2.2.19.tar.gz
    cd httpd-2.2.19
    ./configure --prefix=/app/apache --enable-rewrite --enable-libxml
    make
    make install
    cd ..
    
    # php
    // Go go : http://www.php.net/get/php-5.3.6.tar.gz/from/a/mirror
    curl http://us2.php.net/get/php-5.3.6.tar.gz/from/us.php.net/mirror -O
    mv mirror php.tar.gz
    tar xzvf php.tar.gz
    cd php-5.3.6/
    ./configure --prefix=/app/php  --enable-xslt --with-xsl --with-dom=/app/php --with-dom-xslt=/app/php  --with-iconv --with-curl=/usr/lib --enable-libxml 
    make
    make install
    make
    make install
    cd ..
    
    # php extensions
    # mkdir /app/php/ext
    # cp /usr/lib/libmysqlclient.so.15 /app/php/ext/
    
    # pear
    # apt-get install php5-dev php-pear
    # pear config-set php_dir /app/php
    # pecl install apc
    # mkdir /app/php/include/php/ext/apc
    # cp /usr/lib/php5/20060613/apc.so /app/php/ext/
    # cp /usr/include/php5/ext/apc/apc_serializer.h /app/php/include/php/ext/apc/
    
    
    # package
    cd /app
    # echo '2.2.19' > apache/VERSION
    tar -zcvf apache.tar.gz apache
    # echo '5.3.6' > php/VERSION
    tar -zcvf php.tar.gz php


Hacking
-------

To change this buildpack, fork it on Github. Push up changes to your fork, then create a test app with --buildpack <your-github-url> and push to it.


Meta
----

Created by Pedro Belo.
Many thanks to Keith Rarick for the help with assorted Unix topics :)
