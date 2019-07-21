FROM nginx:1.17
LABEL author "Melvin Versluijs <https://github.com/melvinversluijs>"
RUN apt-get -y update

COPY ./wordpress/ /code
COPY ./docker/certificates /etc/nginx/certs
COPY ./docker/nginx/site.conf /etc/nginx/conf.d/site.conf