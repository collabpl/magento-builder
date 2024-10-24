FROM magento/magento-cloud-docker-php:8.3-cli-1.4.0

ARG COMPOSER_VERSION=2.7.0
ENV ENABLE_SENDMAIL false
ENV PHP_EXTENSIONS bcmath bz2 calendar exif gd gettext intl mysqli opcache pdo_mysql redis soap sockets sodium sysvmsg sysvsem sysvshm xsl zip pcntl

RUN npm install -g ci

ENTRYPOINT ["/docker-entrypoint.sh"]