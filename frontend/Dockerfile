FROM node:15.11.0-alpine
MAINTAINER KIMDONGJANG

RUN mkdir /frontend
WORKDIR /frontend
ENV PATH /frontend/node_modules/.bin:$PATH
COPY package.json .

RUN npm install --no-cache
#RUN apk add --no-cache git

CMD ["npm", "build"]