https://kubernetes.io/zh-cn/docs/tasks/run-application/run-stateless-application-deployment/

## Build
```
docker build -t myclusterregistry.azurecr.io/nginx:v1 .
```

* Dockerfile
```
FROM nginx:latest

#COPY nginx.conf /etc/nginx

#RUN apt-get update \
#    && apt-get upgrade \
#    && apt-get --update add logrotate \
#    && apt-get add --no-cache openssl \
#    && apt-get add --no-cache bash

#RUN apt-get add --no-cache curl

#RUN set -x ; \
#    addgroup -g 82 -S www-data ; \
#    adduser -u 82 -D -S -G www-data www-data && exit 0 ; exit 1

ARG PHP_UPSTREAM_CONTAINER=php-fpm
ARG PHP_UPSTREAM_PORT=9000

# Set upstream conf and remove the default conf
RUN echo "upstream php-upstream { server ${PHP_UPSTREAM_CONTAINER}:${PHP_UPSTREAM_PORT}; }" > /etc/nginx/conf.d/upstream.conf \
    && rm /etc/nginx/conf.d/default.conf

WORKDIR /var/www

EXPOSE 80 443
```


```
apiVersion: apps/v1

kind: Deployment

metadata:

  name: nginx-deployment

spec:

  selector:

    matchLabels:

      app: nginx

  replicas: 2

  template:

    metadata:

      labels:

        app: nginx

    spec:

      containers:

      - name: nginx

        image: nginx:1.16.1 # 将 nginx 版本从 1.14.2 更新为 1.16.1

        ports:

        - containerPort: 80
        env: 
          - name: PHP_UPSTREAM_CONTAINER
            value: "php-fpm"
          - name: PHP_UPSTREAM_PORT
            value: "9000"

```
