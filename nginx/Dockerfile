# LEMP stack as a docker container
FROM ubuntu:14.04
MAINTAINER Daniel Watrous <email>
#ENV http_proxy http://proxy.example.com:8080
#ENV https_proxy https://proxy.example.com:8080

# install nginx
RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get -y install nginx
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN mv /etc/nginx/sites-available/default /etc/nginx/sites-available/default.bak
COPY default /etc/nginx/sites-available/default

# install PHP
RUN apt-get -y install php5-fpm php5-mysql
RUN sed -i s/\;cgi\.fix_pathinfo\s*\=\s*1/cgi.fix_pathinfo\=0/ /etc/php5/fpm/php.ini

# prepare php test scripts
RUN echo "<?php phpinfo(); ?>" > /usr/share/nginx/html/info.php
ADD wall.php /usr/share/nginx/html/wall.php

# add volumes for debug and file manipulation
VOLUME ["/var/log/", "/usr/share/nginx/html/"]

EXPOSE 80

CMD service php5-fpm start && nginx