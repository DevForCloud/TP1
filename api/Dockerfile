FROM node:alpine

WORKDIR /app

COPY package*.json ./
RUN npm install 

COPY . .

CMD ["node", "src/index.js"]

# pour construire l'image : docker build -t api-tp1 .
# pour lancer le conteneur : docker run -p 3000:3000 api-tp1