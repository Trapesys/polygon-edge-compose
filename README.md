# Polygon Edge docker-compose / docker-stack deployment

## Overview
This docker compose file simplifies the deployment of [Polygon Edge](https://github.com/0xPolygon/polygon-edge) in containerized environment.
The trouble with this deployment is that the chain needs to be initialized before the server can be started. 
Before starting the chain two worker containers are started so that the chain can be initialized and destroyed after the job is done.
Blockchain data and `genesis.json` are persisted with volumes bind mounts.

## Usage
### Prequestites
`docker` and `docker-compose`

Clone repo or simply copy paste `docker-compse.yaml` and run docker-compose up. Docker compose [docs](https://docs.docker.com/compose/)
This will start a chain with default parameters.
You should be able to interact with the chain on the default http port ( port 80 )
To test this run `curl localhost`, you should get a responce `Polygon Edge JSON-RPC`

## Customisation

### Genesis
You can customise the genesis.json file parameters, by adding your own parameters to the `command: ["-mode","genesis"]`.
The available options are:
```
-num-nodes ( default 4 )
-premine account:ammount
-chain-id ( default 5100 )
-chain-name ( default polygon-edge )
-block-gas-limit
-epoch-size
```
the rest are defaults from [genesis](https://edge-docs.polygon.technology/docs/get-started/cli-commands#genesis-flags) command.

For example, if we would like to set chain name the command for `genesis-ledge` container would be `command: ["-mode","genesis","-chain-name","my-awsome-chain"]`.

### Server
To customize server command follow the cli commands [docs](https://edge-docs.polygon.technology/docs/get-started/cli-commands#server-flags).
For every node, you can add additional arguments to the `command: ` field.


### Proxy
The additional container is nginx proxy with very basic config file, bind mounted for easy configuration.
Nginx is proxying JSON-RPC requests to all 4 nodes with round-robin method.
You can easily configure this config file to suit your needs.
