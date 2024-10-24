FROM magento/magento-cloud-docker-php:8.3-cli-1.4.0

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

RUN npm install -g puppeteer --unsafe-perm=true ci

RUN /docker-entrypoint.sh