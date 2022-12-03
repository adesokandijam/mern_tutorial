FROM node:alpine as build
WORKDIR /app
COPY package.json /app/
RUN npm install 
COPY . /app
RUN npm run build

FROM nginx:1.16.0

COPY --from=build /app/build /usr/share/nginx/html

RUN rm /etc/nginx/conf.d/default.conf

COPY nginx/nginx.conf /etc/nginx/conf.d

EXPOSE 80

# Start Nginx server
CMD ["/bin/bash", "-c", "nginx -g \"daemon off;\""]