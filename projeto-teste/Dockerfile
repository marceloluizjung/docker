#Imagem base
FROM node

#Diretório de trabalho (aonde é que a imagem vai ser executada)
WORKDIR /app

#Copia os .json e cola dentro da pasta app
COPY *.json /app

#Instala as dependências do projeto
RUN npm install

#Copia tudo e cola dentro da pasta app
COPY . /app

#Expõe a porta da aplicação
EXPOSE 3000

#Executa a aplicação
CMD [ "node", "app.js" ]
