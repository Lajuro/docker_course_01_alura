# Imagem do Node v14
FROM node:14

# Definimos que a pasta /app-nodejs será a pasta de trabalho dentro da imagem
WORKDIR /app-node

# Copiamos da pasta atual para a pasta definida no WORKDIR
COPY . .

# Rodamos o comando npm install
RUN npm install

# Definimos que o comando de entrada será o abaixo
ENTRYPOINT npm start .
