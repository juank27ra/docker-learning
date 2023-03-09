docker container run \
--name nest-app \
-w //app \
-p 80:3000 \
-v "$(pwd)"://app \
node:16-alpine3.16 \
sh -c "yarn install && yarn start:dev"


-w working directori, es para hacer un cd dentro del contenedor 

-v volumen 
node:16 es la imagen 
sh -c tan pronto la imagen se monta quiero ejecutar un shel command para ejecutar lo que está en ""