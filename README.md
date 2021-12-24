# docker_nginx_express_react_test

## dependency

### backend
express 4.17.1

nodemon 2.0.7

### frontend
axios: 0.21.1

react: 17.0.2

react-dom: 17.0.2

react-scripts: 5.0.0

web-vitals: 2.1.2

### nginx
nginx latest



## configuration
### backend-Dockerfile
```
FROM node:15.11.0-alpine
MAINTAINER KIMDONGJANG

RUN mkdir /app
WORKDIR /app
ENV PATH /app/node_modules/.bin:$PATH
COPY package.json /app/package.json

RUN npm install --no-cache
#RUN apk add --no-cache git

COPY . /app
CMD ["npm", "run", "server"]
```


### docker-compose.yml
```
version: '3.3'

services:
  nginx_proxy:
    image: nginx:latest
    container_name: nginx_proxy
    restart: "on-failure"
    ports:
      - 80:80
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf
      - ./frontend/build:/usr/share/nginx/html

  server:
    build:
      context: ./backend/
    container_name: server
    restart: "on-failure"
    expose:
      - 8080
    volumes:
      - './backend:/app'
      - '/app/node_modules'
    environment:
      - NODE_ENV=development
      - CHOKIDAR_USEPOLLING=true
    stdin_open: true
    tty: true
```

### package.json
내부 소스 참고

