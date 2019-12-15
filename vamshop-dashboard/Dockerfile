FROM node:8
LABEL maintainer "Nitin Goyal <nitingoyal.dev@gmail.com>, Luke Busstra <luke.busstra@gmail.com>, VamShop <vamshop@gmail.com>"

ENV NGINX_CODENAME stretch
ENV VAMSHOP_VERSION 0.36.0

# install requirements and NGINX
RUN echo "deb http://nginx.org/packages/debian/ ${NGINX_CODENAME} nginx" >> /etc/apt/sources.list \
	&& apt-get update && apt-get install --no-install-recommends --no-install-suggests -y --force-yes \
		bash \
		zip \
		unzip \
		wget \
		curl \
		nano \
		ca-certificates \
		nginx

# download project
RUN mkdir -p /var/www \
    && cd /var/www \
    && wget -O vamshop-dashboard.zip https://github.com/vamshop/vamshop-dashboard/archive/$VAMSHOP_VERSION.zip \
    && unzip vamshop-dashboard.zip \
    && rm vamshop-dashboard.zip \
    && mv vamshop-dashboard-$VAMSHOP_VERSION vamshop-dashboard

# Nginx config
RUN cd /var/www/vamshop-dashboard \
	&& mv nginx/nginx.conf /etc/nginx/ \
	&& mv nginx/default.conf /etc/nginx/conf.d/

# script to run Nginx and PM2
RUN cd /var/www/vamshop-dashboard \
	&& cp ./docker-entrypoint.sh /usr/local/bin/ \
	&& chmod +x "/usr/local/bin/docker-entrypoint.sh"

# build project
RUN cd /var/www/vamshop-dashboard \
	&& npm install \
	&& npm cache clean --force \
	&& npm run build

WORKDIR /var/www/vamshop-dashboard

EXPOSE 80

# start env build and Nginx
ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]

