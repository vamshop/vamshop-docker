# Supported tags and respective Dockerfile links

- ```0.34.0```,```0.35.0```, ```latest```
[(0.35.0/Dockerfile)](https://github.com/vamshop/vamshop-docker/blob/v0.35.0/vamshop-dashboard/Dockerfile)
[(0.34.0/Dockerfile)](https://github.com/vamshop/vamshop-docker/blob/v0.34.0/vamshop-dashboard/Dockerfile)


# What is VamShop?
[VamShop](https://github.com/vamshop/vamshop-api) is React and Node.js based eCommerce platform.

# How to use this image

### Start a vamshop-dashboard server instance

#### With Port ***3002****

```shell
docker run -d \
--name vamshop-dashboard \
-p 3002:80 \
vamshop/vamshop-dashboard:latest
```

### Environment variables

Name|Description|Default
-|-|-
`LANGUAGE`|Language|`en`
`API_BASE_URL`|API domain|`http://localhost:3001/api/v1`
`DEVELOPER_MODE`|Developer Mode|`true`

### Image contains

- **Node.js (8.10)** to run
ADMIN on **port 3002** .
- **Nginx (1.12.2)** as a reverse proxy admin. **Port 80**.
