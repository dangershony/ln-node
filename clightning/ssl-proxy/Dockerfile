
FROM nginx

RUN openssl req -x509 -newkey rsa:4096 -keyout /etc/ssl/private/selfsigned.key -out /etc/ssl/certs/selfsigned.crt -days 365 -subj '/CN=localhost' -nodes

ADD nginx.conf /etc/nginx

EXPOSE 3002
