FROM magento/magento-cloud-docker-php:8.2-cli-1.3.5

ENV ENABLE_SENDMAIL false
ENV COMPOSER_VERSION 2.2.23
ENV PHP_EXTENSIONS bcmath bz2 calendar exif gd gettext intl mysqli pcntl pdo_mysql soap sockets sysvmsg sysvsem sysvshm opcache zip redis xsl sodium

RUN apt-get update \
  && chown root:root /var/log \
  && apt-get upgrade -y \
  && apt-get install -y --no-install-recommends \
  libnss3 \
  libxss1 \
  libasound2 \
  libatk-bridge2.0-0 \
  libgtk-3-0 \
  libgbm-dev \
  libx11-xcb1 \
  libxtst-dev \
  && rm -rf /var/lib/apt/lists/*

RUN npm install -g puppeteer --unsafe-perm=true magepack --no-optional

RUN /docker-entrypoint.sh