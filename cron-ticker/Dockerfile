FROM node:19.2-alpine3.16
# /app

# cd app     nos movemos a este directorio que viene ya preinstalado con node 
WORKDIR /app

#    los archivos que quiero copiar y el destino (sourse dest)
COPY app.js package.json ./

# instalar dependencias 
RUN npm install

# comando run de la imagen 
CMD ["node", "app.js"]


# para construir la imagen generamos el sgte comando 
# docker build --tag cron-ticker .          o tambien   docker build --tag cron-ticker:alpine3.16 .

# docker image ls 
# docker container run cron-ticker          vemos aqui correr nuestra imagen o app en el contenedor


