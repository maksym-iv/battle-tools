FROM alpine:3.15

# Go tools
ARG BOMBARDIER_VERSION=github.com/codesenberg/bombardier@v1.2.5

# Go vars
ENV GOROOT /usr/lib/go
ENV GOPATH /gopath
ENV GOBIN /gopath/bin
ENV PATH $PATH:$GOROOT/bin:$GOPATH/bin

# hadolint ignore=DL3003, DL3018, SC2086, DL3013, DL3018, DL3042
RUN apk --no-cache update && apk --no-cache upgrade \
    && apk --no-cache add ca-certificates \
    # Python
    && apk --no-cache add python3 \
    && python3 -m ensurepip \
    && pip3 install --no-cache --upgrade pip setuptools \
    # Python tools
    && pip install \
        siege-engine \
    # Go
    && apk --no-cache add --virtual build-dependencies go \
    # Go tools
    # Install bombardier
    && echo "Starting installing bombardier $BOMBARDIER_VERSION." \
    && go get ${BOMBARDIER_VERSION} \
    # Cleanup
    && apk del build-dependencies \
    && rm -rf ${GOPATH}/pkg/
