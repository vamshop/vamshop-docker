# Supported tags and respective Dockerfile links

- ```0.33.0```, ```0.34.0```, ```0.35.0```, ```latest```
[(0.35.0/Dockerfile)](https://github.com/vamshop/vamshop-docker/blob/v0.35.0/vamshop-api/Dockerfile)
[(0.34.0/Dockerfile)](https://github.com/vamshop/vamshop-docker/blob/v0.34.0/vamshop-api/Dockerfile)
[(0.33.0/Dockerfile)](https://github.com/vamshop/vamshop-docker/blob/v0.33.0/vamshop-api/Dockerfile)


# What is VamShop?
[VamShop](https://github.com/vamshop/vamshop-api) is React and Node.js based eCommerce platform.

# How to use this image

### Start a vamshop-api server instance

#### With Port ***3001****

```shell
docker run -d \
--name vamshop-api \
-p 3001:80 \
vamshop/vamshop-api:latest
```

#### With Port ***3001**** & Mongodb

```shell
docker run -d \
--name vamshop-api \
-p 3001:80 \
-e DB_HOST=255.255.255.255 \
-e DB_PORT=27017 \
-e DB_NAME=shop \
-e DB_USER= \
-e DB_PASS= \
vamshop/vamshop-api:latest
```

#### With Port ***3001****, Mongodb & Volume

```shell
docker run -d \
--name vamshop-api \
-p 3001:80 \
-e DB_HOST=255.255.255.255 \
-e DB_PORT=27017 \
-e DB_NAME=shop \
-e DB_USER= \
-e DB_PASS= \
-v /var/www/vamshop-on-host:/var/www/vamshop-api \
vamshop/vamshop-api:latest
```

### Environment variables

Name|Description|Default
-|-|-
`LANGUAGE`|Language|`en`
`DB_HOST`|MongoDB host name or IP|`127.0.0.1`
`DB_PORT`|MongoDB server port|`27017`
`DB_NAME`|MongoDB database name|`shop`
`DB_USER`|MongoDB user name|
`DB_PASS`|MongoDB user password|
`DB_URL`|Optional Mongodb URL|
`API_BASE_URL`|API domain|`http://localhost:3001/api/v1`
`STORE_URL`|Store domain|`http://localhost:3000`
`ADMIN_BASE_URL`|Admin domain|`http://localhost:3002`
`ASSETS_BASE_URL`|Assets domain|`http://localhost:3001`
`JWT_SECRET_KEY`|Secret token key|`-`
`COOKIE_SECRET_KEY`|Secret cookie key|`-`


### Image contains

- **Node.js (8.10)** to run
API on **port 3001** .
- **Nginx (1.12.2)** as a reverse proxy to Node.js and dynamic image thumbnails. **Port 80**.
