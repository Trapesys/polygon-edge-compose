FROM alpine:latest

# get branch name from input variable
ARG GIT_BRANCH
ENV git_branch=${GIT_BRANCH}

# Get GO and set GOPATH
COPY --from=golang:1.17-alpine /usr/local/go/ /usr/local/go/
ENV PATH $PATH:/usr/local/go/bin

# Install Polygon Edge from the specified branch
RUN apk add git bash --update --no-cache
RUN git clone https://github.com/0xPolygon/polygon-edge -b ${git_branch} /polygon-edge
RUN cd /polygon-edge && go build -o /usr/local/bin/polygon-edge . && rm -R /polygon-edge

# Remove apk install cache
RUN rm -rf /var/cache/apk/*

# Expose json-rpc, libp2p and grpc ports
EXPOSE 8545 9632 1478

# Run polygon-edge binary when starting the container
ENTRYPOINT ["polygon-edge"]

