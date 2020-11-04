
FROM nginx

RUN apt-get update -y \
    && apt-get install -y \
    build-essential  \
    git  \
    net-tools  

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -  \
  && apt-get install -y \
    nodejs \
    certbot \
    python-certbot-nginx \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Add Tini
ENV TINI_VERSION v0.19.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini

RUN git clone https://github.com/Ride-The-Lightning/RTL.git

WORKDIR /RTL

# Install dependencies
RUN npm install --only=prod

RUN openssl req -x509 -newkey rsa:4096 -keyout /etc/ssl/private/selfsigned.key -out /etc/ssl/certs/selfsigned.crt -days 365 -subj '/CN=localhost' -nodes

ADD RTL-Config.json /RTL

ADD nginx.conf /etc/nginx

EXPOSE 3000
EXPOSE 3002

ADD entrypoint.sh /usr/local/bin
RUN chmod +x /usr/local/bin/entrypoint.sh

ENTRYPOINT ["/tini", "-g", "--"]
#, "/usr/local/bin/entrypoint.sh"]

#RUN systemctl enable nginx

CMD ["node", "rtl"]
