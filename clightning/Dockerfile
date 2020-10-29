FROM dangershony/signet:0.20.1

RUN apt-get update -y \
    && apt-get install -y \
    autoconf \
    automake  \
    build-essential  \
    git  \
    libtool  \
    libgmp-dev \
    libsqlite3-dev  \
    python python3  \
    net-tools  \
    zlib1g-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN git clone https://github.com/ElementsProject/lightning.git

WORKDIR /lightning

RUN ./configure

RUN make install

EXPOSE 9735 9835

CMD ["lightningd"]
