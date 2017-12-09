FROM ubuntu:16.04

RUN apt-get update && apt-get install -y software-properties-common language-pack-en-base \
	&& LC_ALL=en_US.UTF-8 add-apt-repository -y ppa:ondrej/php \
	&& apt-get update \
	&& apt-get install -y php7.0 php7.0-fpm php7.0-mysql mcrypt php7.0-gd curl \
		supervisor \
		php7.0-curl php7.0-mbstring \
		php7.0-mcrypt \
		php7.0-curl \
		php7.0-gd \
		php7.0-gmp \
		php7.0-cli \
		php7.0-curl \
		php7.0-zip \
		php7.0-mb \
		wget \
		zip \
		unzip \
		&& mkdir /run/php \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

RUN sed -i -e 's/listen = \/run\/php\/php7.0-fpm.sock/listen = 0.0.0.0:9000/g' /etc/php/7.0/fpm/pool.d/www.conf \
    && sed -i -e 's/;daemonize = yes/daemonize = no/g' /etc/php/7.0/fpm/php-fpm.conf




RUN { \
		echo 'file_uploads = On'; \
		echo 'memory_limit = 2G'; \
		echo 'upload_max_filesize = 10G'; \
		echo 'post_max_size = 10G'; \
		echo 'max_execution_time = 600'; \
		echo 'opcache.enable = 0'; \

	} >> /etc/php/7.0/fpm/php.ini

RUN { \
		echo 'log_errors = On'; \
		echo 'display_errors = On'; \
		echo 'error_reporting = E_ALL'; \
	} >> /etc/php/7.0/fpm/php.ini



VOLUME /var/www/html

EXPOSE 9000

CMD ["/usr/bin/supervisord"]
