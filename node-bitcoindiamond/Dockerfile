FROM magnumwallet/base-full

VOLUME ["/mnt/data/"]
SHELL ["/bin/bash", "-c"]

# ----

WORKDIR /opt
RUN git clone https://github.com/eveybcd/BitcoinDiamond.git
RUN mv BitcoinDiamond node

WORKDIR /opt/node
RUN ./autogen.sh
RUN ./configure  --without-gui
RUN make -j$(nproc)

RUN ln -s /opt/node/src/bitcoindiamondd /opt/node/src/node

# ----

COPY ./data /opt/data/
WORKDIR /opt/data

# ----

COPY entrypoint.sh /usr/local/bin/
COPY cmd.sh /usr/local/bin/

ENTRYPOINT ["entrypoint.sh"]
CMD ["cmd.sh", ""]
