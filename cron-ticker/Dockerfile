#  docker buildx build --platform linux/amd64,linux/arm64,linux/arm/v7 \
#   -t <username>/<image>:latest --push .

#    docker buildx build --platform linux/amd64,linux/arm64,linux/arm/v7 \
#   -t juank27/cron-ticker:latest --push .

# FROM --platform=linux/amd64 node:19.2-alpine3.16
# FROM --platform=$BUILDPLATFORM node:19.2-alpine3.16
# FROM --platform=arm64 node:19.2-alpine3.16
# FROM node:19.2-alpine3.16
FROM --platform=$BUILDPLATFORM node:19.2-alpine3.16 as deps
WORKDIR /app
COPY package.json ./
# instalar dependencias de desarrollo
RUN npm install


FROM --platform=$BUILDPLATFORM node:19.2-alpine3.16 as builder
WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY . .
RUN npm run test
# RUN npm run build


FROM --platform=$BUILDPLATFORM node:19.2-alpine3.16 as prod-deps
WORKDIR /app
COPY package.json ./
RUN npm install --prod


FROM --platform=$BUILDPLATFORM node:19.2-alpine3.16 as runner
WORKDIR /app
# copiar todo lo que está en mi proyecto (basado en el patha del dockerfile) y lo pega en el workdir excluyendo lo que está en el dockerignore
COPY --from=prod-deps /app/node_modules ./node_modules
COPY app.js ./
COPY tasks ./tasks
# comando run de la imagen o comando con el que vamos a iniciar la imagen 
CMD ["node", "app.js"]


# para construir la imagen generamos el sgte comando 
# docker build --tag cron-ticker .          o tambien   docker build --tag cron-ticker:alpine3.16 .

# docker image ls 
# docker container run cron-ticker          vemos aqui correr nuestra imagen o app en el contenedor


