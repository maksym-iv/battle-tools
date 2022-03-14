FROM alpine:3.15

# Go vars
ENV GOROOT /usr/lib/go
ENV GOPATH /gopath
ENV GOBIN /gopath/bin
ENV PATH $PATH:$GOROOT/bin:$GOPATH/bin

# hadolint ignore=DL3003, DL3018, SC2086, DL3013, DL3018, DL3042
RUN apk --no-cache update && apk --no-cache upgrade \
    && apk --no-cache add ca-certificates \
    && apk --no-cache add --virtual build-dependencies go git \
    # Python
    && apk --no-cache add python3 python3-dev \
        linux-headers \
        libffi-dev \
    && python3 -m ensurepip \
    && pip3 install --no-cache --upgrade pip setuptools \
    # Python tools
    && pip install \
        siege-engine \
    # Install MHDDoS
    && git clone https://github.com/MHProDev/MHDDoS.git \
    && cd MHDDoS \
    && pip install -r requirements.txt \
    # Go
    # Go tools
    # Install bombardier
    && echo "Starting installing bombardier" \
    && go get github.com/codesenberg/bombardier@v1.2.5 \
    # Install bilalcaliskan/syn-flood
    && echo "Starting installing syn-flood" \
    && go get github.com/bilalcaliskan/syn-flood \
    # Install rakyll/hey
    && echo "Starting installing hey" \
    && go get github.com/rakyll/hey \
    # Cleanup
    && apk del build-dependencies \
    && rm -rf ${GOPATH}/pkg/
