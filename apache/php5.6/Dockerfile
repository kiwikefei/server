FROM debian:jessie
MAINTAINER kiwikefei@gmail.com

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get -qq update

# essential packages 
RUN apt-get -qqy install sudo wget lynx telnet vim curl make git-core locales bzip2 htop

RUN echo "LANG=en_US.UTF-8\n" > /etc/default/locale && \
	echo "en_US.UTF-8 UTF-8\n" > /etc/locale.gen && \
	locale-gen

ENV LANG en_US.UTF-8

RUN apt-get -qqy install apache2 \
	php5-cli libapache2-mod-php5 php5-mysqlnd \
    php5-mcrypt php5-tidy php5-curl php5-gd php-pear

RUN	wget https://getcomposer.org/composer.phar && \
	chmod +x composer.phar && \
	mv composer.phar /usr/local/bin/composer

RUN a2enmod rewrite && \
	a2enmod expires && \
	rm -r /var/www/html && \
	echo "date.timezone = Pacific/Auckland" > /etc/php5/apache2/conf.d/timezone.ini && \
	echo "date.timezone = Pacific/Auckland" > /etc/php5/cli/conf.d/timezone.ini

COPY ./conf/000-default.conf /etc/apache2/sites-available/000-default.conf
COPY ./conf/laravel.test.conf /etc/apache2/sites-available/laravel.test.conf
COPY ./conf/silverstripe.test.conf /etc/apache2/sites-available/silverstripe.test.conf
RUN rm -f /etc/apache2/sites-enabled/*
RUN ln -s /etc/apache2/sites-available/*.conf /etc/apache2/sites-enabled/
COPY ./bootstrap /usr/local/bin/bootstrap
RUN chmod +x /usr/local/bin/bootstrap

EXPOSE 80

VOLUME /var/www

WORKDIR /var/www

CMD ["/usr/local/bin/bootstrap"]