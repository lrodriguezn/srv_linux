

# Instalación de traefik
## Video y documentación
[Video instalar traefik](https://www.youtube.com/watch?v=QMpe-8woTxg&t=1151s)
[Pagina paso a paso](https://www.nosolohacking.info/traefik/)
[GitHub LuisG](https://github.com/lrodriguezn/srv_linux/blob/master/traefik.md)

## Pasos

 - Actualizar instancia
>    sudo apt update
 - Crear directorio donde se copiaran todos los archivos de configuracion de traefik
 >   mkdir traefik \
 >   cd traefik

 - Crear archivo de docker-compose.ymal, y actualizar la URL que se utilizara para ingresar a traefik, ej: traefik.lgyss.click
 >   nano docker-compose.yaml

 - Crear archivo cloudflare_token.txt que tendra el token generado en cloudflere.
 >   nano cloudflare_token.txt
 BMrtSm5AfGjdrUjYzgtcR2agmbtkugMZVvm3JkjC

 - Crear archivo .env para crear la variable CREDENCIALES_DASHBOARD con el usuario y pass generado htpasswd que se usara para ingresar al dashboard
[Pagina para generar credenciales](https://www.web2generators.com/apache-tools/htpasswd-generator)
Donde encuentre un $ se debe agregar uno adicionar para que quede \$\$\
clave htpasswd para(Lgyss3216*): 
lgyss:\$\$apr1\$\$o7s9ia5p\$\$7Ovc5Cwd.DS1O8GBosjbE0
 >   nano .env \
 >   CREDENCIALES_DASHBOARD=lgyss:\$\$apr1\$\$o7s9ia5p\$\$7Ovc5Cwd.DS1O8GBosjbE0

 - Crear archivo acme.json en el directorio /datos y darle permiso de escritura para que se guarde el certificado de seguridad let's encrypt

> cd datos \
> touch acme.json \
> chmod 600 acme.json

- Iniciar el docker compose. Debemos quedar en el directorio traefik

> docker network create proxy    --Esto permite crear un network usada en el docker-compose \
> docker compose up -d \
> docker ps \
> docker logs #contenedor \
> ss -nltp   --permite validar si el docker esta escuchando en el puerto 80

 - probar la respuesta del contenedor traefik.lgyss.click
 - Comprobar que el sitio genero el certificado
> cd datos \
> nano acme.json

- Si el archivo acme.json genero el certificado se debe cambiar a utilizar el certificado de produccion
> cd datos \
> rm acme.json \
> touch acme.json \
> chmod 600 acme.json \
> nano traefik.yml \
> caServer: https://acme-v02.api.letsencrypt.org/directory # Servidor ACME de Let's Encrypt (producción) \
> #caServer: https://acme-staging-v02.api.letsencrypt.org/directory # Servidor ACME de Let's Encrypt para pruebas (opcional)
