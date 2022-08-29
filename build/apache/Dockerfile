FROM ubuntu:focal

RUN apt-get update \
    && apt-get install apt-utils -y \
    && DEBIAN_FRONTEND=noninteractive TZ=Europe/Berlin apt-get install -y \
    net-tools \
    zip \
    unzip \
    apache2 \
    joe \
    build-essential \
    git
    

COPY security.conf /etc/apache2/conf-enabled/security.conf
COPY 001-sugar.conf /etc/apache2/sites-available/001-sugar.conf
COPY ports.conf /etc/apache2/ports.conf

RUN set -ex \
    && a2dismod	mpm_event \
    && a2enmod access_compat actions alias auth_basic authn_core authn_file authz_core authz_groupfile authz_host authz_user autoindex cgid deflate dir env expires filter headers mime mpm_worker negotiation proxy proxy_fcgi reqtimeout rewrite setenvif socache_shmcb ssl status \
    && a2dissite 000-default \
    && a2ensite 001-sugar
    

RUN mkdir /var/www/html/sugar && echo "<?php \nphpinfo() \n?>" > /var/www/html/sugar/index.php && chown -R www-data:www-data /var/www/html/sugar
RUN chown -R www-data:www-data /var/www/html

WORKDIR /var/www/html/sugar

CMD ["/usr/sbin/apache2ctl","-DFOREGROUND"]