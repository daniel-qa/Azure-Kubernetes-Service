
* nginx.yaml
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: myclusterregistry.azurecr.io/nginx:v1
        ports:
        - containerPort: 80        
        # - containerPort: 443
        env: 
          - name: PHP_UPSTREAM_CONTAINER
            value: "php-fpm"               # service name 
          - name: PHP_UPSTREAM_PORT
            value: "9000"
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-svc
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: nginx
```

* dockerfile 
```
FROM nginx:latest

COPY nginx.conf /etc/nginx

RUN apt-get update && apt-get -y install logrotate \
		&& apt-get install openssl \
		&& apt-get install bash	

RUN apt-get install curl -y


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
