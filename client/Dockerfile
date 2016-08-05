#
# Gulp image
#

FROM node:5.7

MAINTAINER Fabien D. <fabien@myprod.net>

RUN apt-get update && apt-get install -y --no-install-recommends \
    rubygems build-essential ruby-dev \
    && rm -rf /var/lib/apt/lists/*

# Install Gulp & Bower
#RUN npm install -gq gulp bower

# Install Gem Sass Compass
RUN gem install sass

RUN usermod -u ${DOCKER_USER_ID:-1000} www-data \
    && mkdir -p ${APP_BASE_DIR:-/var/www/}

#WORKDIR ${APP_BASE_DIR:-/var/www/}
WORKDIR /app
RUN git clone https://github.com/derdiedasjojo/platform-client && cd platform-client && git checkout v3.4.7-cam
RUN	cd platform-client && npm install -g gulp

ENV BACKEND_URL=http://138.201.159.97:8080/api/v3/
RUN export BACKEND_URL=http://138.201.159.97:8080/api/v3/

RUN cd platform-client && npm install
ADD platform-pattern-library/* /app/platform-client/node_modules/platform-pattern-library/

ENV BACKEND_URL=http://138.201.159.97:8080
RUN export BACKEND_URL=http://138.201.159.97:8080

RUN cd platform-client && gulp build
#RUN mkdir -p /usr/share/nginx/html && cp -r /app/platform-client/server/www/* /usr/share/nginx/html/
#VOLUME /usr/share/nginx/html
RUN apt-get update && apt-get install -y vim-tiny nginx
ADD nginx-site.conf /etc/nginx/sites-available/default

# Install Gulp
#RUN npm install gulp
#WORKDIR /usr/share/nginx/html

#VOLUME /app/platform-client/server
#WORKDIR /app/platform-client
#CMD gulp
CMD nginx -g 'daemon off;'
