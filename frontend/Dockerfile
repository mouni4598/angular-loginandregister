# Use a Node.js 14 image as the builder
FROM node:14-alpine as builder

WORKDIR /usr/src/app
COPY package.json package-lock.json ./
RUN npm install
COPY . .
RUN npm run build --silent

# Use an Nginx image for the final container
FROM nginx:1.17.1-alpine
VOLUME /var/cache/nginx
COPY --from=builder /usr/src/app/dist/frontend /usr/share/nginx/html
COPY nginx.conf /etc/nginx/nginx.conf
EXPOSE 80

