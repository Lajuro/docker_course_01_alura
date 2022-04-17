# Imagem do Node v14
FROM node:14

# Definimos que a pasta /app-nodejs será a pasta de trabalho dentro da imagem
WORKDIR /app-node

# Criamos uma variável de ambiente que irá definir a porta, existe apenas em tempo de execução
ARG PORT=6000

# Definirá como uma variável de ambiente da imagem
ENV PORT=$PORT

# Informamos a porta do container que será a porta da imagem
EXPOSE $PORT

# Copiamos da pasta atual para a pasta definida no WORKDIR
COPY . .

# Rodamos o comando npm install
RUN npm install

# Definimos que o comando de entrada será o abaixo
ENTRYPOINT npm start .
