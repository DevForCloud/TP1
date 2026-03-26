FROM node:alpine

WORKDIR /app

COPY package*.json ./
RUN npm install 

COPY . .

CMD ["node", "src/index.js"]

# on met le copy après le npm install pour éviter de réinstaller 
# les dépendances à chaque changement de code

# pour construire l'image : docker build -t api-tp1 .
# pour lancer le conteneur : docker run -p 3000:3000 api-tp1