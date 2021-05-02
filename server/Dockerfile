FROM node:15 as base
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .

#FROM base as prod
EXPOSE 3000
CMD [ "npm", "run", "start" ]