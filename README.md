# Supported tags

- ```0.33.0```, ```0.34.0```, ```0.35.0```, ```latest```

#Supported Images

- [vamshop-api](https://github.com/vamshop/vamshop-docker/blob/master/vamshop-api/README.md)
- [vamshop-dashboard](https://github.com/vamshop/vamshop-docker/blob/master/vamshop-dashboard/README.md)
- [vamshop-storefront](https://github.com/vamshop/vamshop-docker/blob/master/vamshop-storefront/README.md)
- [vamshop-proxy](https://github.com/vamshop/vamshop-docker/blob/master/vamshop-proxy/README.md)


# What is VamShop?
[VamShop](https://github.com/vamshop/vamshop-api) is React and Node.js based eCommerce platform.

# docker - How to use this images

### Start a mongo server instance

```shell
docker run -d \
--name store-db \
-v /var/www/store-db:/data/db \
mongo:latest
```

### Start a vamshop-api server instance

```shell
docker run -d \
--name vamshop-api \
--link store-db:db \
-p 3001:80 \
-e DB_HOST=db \
-e DB_PORT=27017 \
-e DB_NAME=shop \
-e DB_USER= \
-e DB_PASS= \
-v /var/www/vamshop-api/public/content:/var/www/vamshop-api/public/content \
vamshop/vamshop-api:latest
```

### Start a vamshop-dashboard server instance

```shell
docker run -d \
--name vamshop-dashboard \
--link vamshop-api:vamshop-api \
-p 3002:80 \
-e API_BASE_URL=http://vamshop/api/vi
vamshop/vamshop-dashboard:latest
```

### Start a vamshop-storefront server instance

```shell
docker run -d \
--name vamshop-storefront \
--link vamshop-api:vamshop-api \
-p 3000:80 \
-e API_BASE_URL=http://vamshop/api/v1 \ 
-e AJAX_BASE_URL=http://vamshop/ajax \ 
vamshop/vamshop-storefront:latest
```

# docker compose - How to use this images

```shell
version: '3'

services:
  vamshop-api:
    image: vamshop/vamshop-api
    ports:
      - 3001:80
    environment:
      - DB_HOST=db
      - DB_PORT=27017
      - DB_NAME=shop
      - DB_USER=
      - DB_PASS=
    volumes:
      - ./content:/var/www/vamshop-api/public/content
    depends_on:
      - db
    restart: always

  vamshop-storefront:
    image: vamshop/vamshop-storefront
    environment:
      - API_BASE_URL=http://vamshop/api/v1
      - AJAX_BASE_URL=http://vamshop/ajax
    ports:
      - 3000:80
    depends_on:
      - vamshop-api
    restart: always

  vamshop-dashboard:
    image: vamshop/vamshop-dashboard
    ports:
      - 3002:80
    depends_on:
      - vamshop-api
    restart: always

  db:
    image: mongo:3.4
    ports:
      - 27017:27017
    volumes:
      - ./db:/data/db
    restart: always
```

### Access

localhost:3000
