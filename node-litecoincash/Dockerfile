FROM magnumwallet/base-full

# ----

VOLUME ["/mnt/data/"]
SHELL ["/bin/bash", "-c"]

# ----

ARG repo=litecoincash-project/litecoincash
ARG platform=x86_64

# ----

WORKDIR /opt
RUN curl -s https://api.github.com/repos/$repo/releases/latest | grep browser_download_url | grep $platform | cut -d '"' -f 4 | wget -qi -
RUN tar -xf `ls -t ./ | head -1` && mv `ls ./ | head -1` node

WORKDIR /opt/node
RUN ln -s `find /opt/node/bin -name "*d" | head -1` /opt/node/bin/node

# ----

COPY ./data /opt/data/
WORKDIR /opt/data

# ----

COPY entrypoint.sh /usr/local/bin/
COPY cmd.sh /usr/local/bin/

ENTRYPOINT ["entrypoint.sh"]
CMD ["cmd.sh", ""]
