FROM node:8
LABEL maintainer "Luke Busstra <luke.busstra@gmail.com>, VamShop <vamshop@gmail.com>"

ENV NGINX_CODENAME stretch

# install requirements and NGINX
RUN echo "deb http://nginx.org/packages/debian/ ${NGINX_CODENAME} nginx" >> /etc/apt/sources.list \
	&& apt-get update && apt-get install --no-install-recommends --no-install-suggests -y --force-yes \
		gettext-base\
		bash \
		nano \
		ca-certificates \
		nginx \
		nginx-module-image-filter

# Nginx config
COPY nginx/nginx.conf /etc/nginx/
COPY nginx/default.conf.template /etc/nginx/conf.d/

# script to run Nginx and PM2
COPY docker-entrypoint.sh /usr/local/bin/
RUN chmod +x "/usr/local/bin/docker-entrypoint.sh"

EXPOSE 80

# start env build and Nginx
ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]
