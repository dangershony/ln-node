
FROM node

RUN apt-get update -y \
    && apt-get install -y \
    git  

ENV TINI_VERSION v0.19.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini

RUN git clone https://github.com/Ride-The-Lightning/RTL.git

WORKDIR /RTL

RUN npm install --only=prod

ADD RTL-Config.json /RTL

EXPOSE 3000

ENTRYPOINT ["/tini", "-g", "--"]

CMD ["node", "rtl"]
