FROM php:5.6.30-apache

RUN apt-get update && \
	apt-get -y upgrade

RUN apt-get -y install mysql-client

# (Re)create snakeoil
RUN openssl req -x509 -nodes -days 1095 -newkey rsa:2048 \
		-keyout /etc/ssl/private/ssl-cert-snakeoil.key\
		-out /etc/ssl/certs/ssl-cert-snakeoil.pem\
		-subj "/C=UK/ST=England/L=Newcastle/O=Nomad Digtal Ltd/OU=R&D/CN=hpdesktop.shabble.co.uk"

RUN a2enmod ssl

# Enable ssl
RUN ln -s /etc/apache2/sites-available/default-ssl.conf /etc/apache2/sites-enabled/000-default-ssl.conf

# mod_rewrite
RUN ln -s /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/rewrite.load

RUN echo "[PHP]\nalways_populate_raw_post_data = -1" >> /usr/local/etc/php/php.ini

RUN docker-php-ext-install bcmath