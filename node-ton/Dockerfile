FROM ubuntu:16.04 as builder
RUN apt update && \
        apt install -y build-essential cmake clang-6.0 openssl libssl-dev zlib1g-dev gperf && \
        rm -rf /var/lib/apt/lists/*
ENV CC clang-6.0
ENV CXX clang++-6.0
WORKDIR /ton
COPY . .
RUN mkdir build && \
        cd build && \
        cmake .. && \
        cmake --build . --target lite-client && \
        cmake --build . --target fift

FROM ubuntu:16.04
RUN apt update && \
        apt install -y openssl && \
        rm -rf /var/lib/apt/lists/*
COPY --from=builder /ton/build/lite-client /usr/local/bin/lite-client
COPY --from=builder /ton/build/crypto/fift /usr/local/bin/
COPY --from=builder /ton/build/crypto/tlbc /usr/local/bin/
#COPY --from=builder /ton/crypto/fift/Asm.fif /usr/include/ton/
#COPY --from=builder /ton/crypto/fift/Fift.fif /usr/include/ton/
COPY ton-lite-client-test1.config.json /etc/ton/
ENV FIFTPATH=/usr/include/ton
WORKDIR /data

COPY entrypoint.sh /usr/local/bin/
COPY cmd.sh /usr/local/bin/

ENTRYPOINT ["entrypoint.sh"]
CMD ["cmd.sh", ""]