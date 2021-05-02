# etapa de compilación
FROM node:lts-alpine3.12 as build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run prod
# etapa de producción
FROM nginx:stable-alpine as production
COPY --from=build /app/out /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]