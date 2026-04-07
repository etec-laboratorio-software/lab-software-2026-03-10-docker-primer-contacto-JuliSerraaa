FROM node:20-alpine

# Instalar sqlite CLI y dependencias necesarias
RUN apk add --no-cache sqlite

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

# Creamos la carpeta data por si no existe
RUN mkdir -p data

EXPOSE 3000

CMD ["node", "server.js"]
