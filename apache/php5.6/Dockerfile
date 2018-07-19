FROM debian:jessie
MAINTAINER kiwikefei@gmail.com

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get -qq update

# essential packages 
RUN apt-get -qqy install sudo wget lynx telnet vim curl make git-core locales bzip2 htop net-tools

RUN echo "LANG=en_US.UTF-8\n" > /etc/default/locale && \
	echo "en_US.UTF-8 UTF-8\n" > /etc/locale.gen && \
	locale-gen

ENV LANG en_US.UTF-8

RUN apt-get -qqy install apache2 \
	php5-cli libapache2-mod-php5 php5-mysqlnd \
    php5-mcrypt php5-tidy php5-curl php5-gd php-pear

RUN apt-get -qqy install php5-xdebug 

RUN	wget https://getcomposer.org/composer.phar && \
	chmod +x composer.phar && \
	mv composer.phar /usr/local/bin/composer

RUN a2enmod rewrite && \
	a2enmod expires && \
	echo "date.timezone = Pacific/Auckland" > /etc/php5/apache2/conf.d/timezone.ini && \
	echo "date.timezone = Pacific/Auckland" > /etc/php5/cli/conf.d/timezone.ini

COPY arizto.test.conf /etc/apache2/sites-available/arizto.test.conf
COPY xdebug.ini /etc/php5/mods-available/xdebug.ini

RUN a2ensite 000-default.conf
RUN a2ensite arizto.test.conf

RUN service apache2 reload

COPY ./bootstrap /usr/local/bin/bootstrap
RUN chmod +x /usr/local/bin/bootstrap

EXPOSE 80

VOLUME /var/www

WORKDIR /var/www

CMD ["/usr/local/bin/bootstrap"]