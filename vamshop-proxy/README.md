# Supported tags and respective Dockerfile links

- ```0.34.0```,```0.35.0```,  ```latest```
[(0.35.0/Dockerfile)](https://github.com/vamshop/vamshop-docker/blob/v0.35.0/vamshop-proxy/Dockerfile)
[(0.34.0/Dockerfile)](https://github.com/vamshop/vamshop-docker/blob/v0.34.0/vamshop-proxy/Dockerfile)


# What is VamShop?
[VamShop](https://github.com/vamshop/vamshop-api) is React and Node.js based eCommerce platform.

# Docker - How to use this image

### Start a vamshop-proxy server instance

#### With Port ***80****

```shell
docker run -d \
--name vamshop-proxy \
-p 80:80 \
-e DOMAIN=example.com \
-e API_HOST=localhost:3001 \
-e STORE_HOST=localhost:3000 \
-e ADMIN_HOST=localhost:3002 \
vamshop/vamshop-proxy:latest
```

# Docker Compose - How to use this image

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
      - STORE_URL=http://www.example.com
      - ADMIN_BASE_URL=http://admin.example.com
      - ASSETS_BASE_URL=http://api.example.com
    volumes:
      - ./content:/var/www/vamshop-api/public/content
    depends_on:
      - db
    restart: always

  vamshop-storefront:
    image: vamshop/vamshop-storefront
    environment:
      - API_BASE_URL=http://api.example.com/api/v1
      - AJAX_BASE_URL=http://api.example.com/ajax
    ports:
      - 3000:80
    depends_on:
      - vamshop-api
    restart: always

  vamshop-dashboard:
    image: vamshop/vamshop-dashboard
    environment:
      - API_BASE_URL=http://api.example.com/api/v1
    ports:
      - 3002:80
    depends_on:
      - vamshop-api
    restart: always

  vamshop-proxy:
    image: vamshop/vamshop-proxy
    environment:
      - DOMAIN=example.com
      - API_HOST=vamshop-api
      - STORE_HOST=vamshop-storefront
      - ADMIN_HOST=vamshop-dashboard
    ports:
      - 80:80
    depends_on:
      - vamshop-api
      - vamshop-storefront
      - vamshop-dashboard
    restart: always

  db:
    image: mongo:3.6
    ports:
      - 27017:27017
    volumes:
      - ./db:/data/db
    restart: always
```

### Environment variables

Name|Description|Default
-|-|-
`DOMAIN`|Language|
`API_HOST`|API Host|
`STORE_HOST`|Store Host|
`ADMIN_HOST`|Admin Host|

### Image contains

- **Nginx (1.12.2)** as a reverse proxy Store at domain.com, admin at admin.domain.com and api at api.domain.com. **Port 80**.
