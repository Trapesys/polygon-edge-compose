# Create Polygon-Edge container from a custom branch

If you would like to create a Polygon Edge container from a custom branch, you need to run an additional step before `docker-compose up` command.

## Build custom container
To build a container from a custom branch run `docker-compose build --build-arg GIT_BRANCH=<branch_name>`.   
After the build is complete a new container named `local/polygon-edge` should be created.

## Run containers
After you've built your custom image `local/polygon-edge`, all you need to do is run `docker-compose up` command or `docker-compose -d` if you'd like the containers to run in the background.    
Consult main readme file on chain customization options.

## Node data directories
By default all node data dirs will be placed in nodes-data directory.   
All nodes are bind mounted for easy access to node data/genesis directories.  
Folder names inside nodes-data directory corespond to container names.

## JSON-RPC
There is no proxy container for JSON-RPC in this docker-compose.  
This means that all JSON-RPC endpoints are exposed on port 1000 + node number.   
For example: `node1` json-rpc can be accessed via `10001` port, `node2` via `10002` port and so on.