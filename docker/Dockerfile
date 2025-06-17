
FROM node:20.5.0-alpine as node

WORKDIR /app

COPY package.json package-lock.json ./
RUN rm package-lock.json
RUN npm cache clean --force
RUN npm install --verbose
COPY . .

RUN npm run build

FROM nginx:alpine

VOLUME /var/cache/nginx 

RUN rm -r /usr/share/nginx/html/*

COPY --from=node /app/dist/angular-https-nginx-remote /usr/share/nginx/html

COPY nginx/nginx.config /etc/nginx/templates/default.conf.template

CMD ["nginx", "-g", "daemon off;"] 
