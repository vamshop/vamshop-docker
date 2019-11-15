# Supported tags and respective Dockerfile links

- ```0.34.0```, ```0.35.0```, ```latest```
[(0.35.0/Dockerfile)](https://github.com/vamshop/vamshop-docker/blob/v0.35.0/vamshop-storefront/Dockerfile)
[(0.34.0/Dockerfile)](https://github.com/vamshop/vamshop-docker/blob/v0.34.0/vamshop-storefront/Dockerfile)


# What is VamShop?
[VamShop](https://github.com/vamshop/vamshop-api) is React and Node.js based eCommerce platform.

# How to use this image

### Start a vamshop-storefront server instance

#### With Port ***3000****

```shell
docker run -d \
--name vamshop-storefront \
-p 3000:80 \
vamshop/vamshop-storefront:latest
```

#### With Port ***3000**** & api connection

```shell
docker run -d \
--name vamshop-storefront \
-p 3000:80 \
-e API_BASE_URL=http://api-host/api/v1 \ 
-e AJAX_BASE_URL=http://api-host/ajax \ 
vamshop/vamshop-storefront:latest
```

### Environment variables

Name|Description|Default
-|-|-
`LANGUAGE`|Language|`en`
`API_BASE_URL`|API domain|`http://localhost:3001/api/v1`
`AJAX_BASE_URL`|AJAX domain|`http://localhost:3001/ajax`
`JWT_SECRET_KEY`|Secret token key|`-`
`COOKIE_SECRET_KEY`|Secret cookie key|`-`

### Image contains

- **Node.js (8.10)** to run
ADMIN on **port 3002** .
- **Nginx (1.12.2)** as a reverse proxy store. **Port 80**.
