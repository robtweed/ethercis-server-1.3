# ethercis-server-1.3

## EtherCIS version 1.3 Server Container

This is based on and derived from the 
[Scottish Digital Health EtherCIS Server Docker Container](https://hub.docker.com/r/nesnds/ethercis-server),
but fixed for operation on a Linux host.

This Docker Container must be used in conjunction with the 
[ethercis-db-1.3](https://github.com/robtweed/ethercis-db-1.3) Container

Prebuilt docker images for both are available on the Docker Hub:

- rtweed/ethercis-db
- rtweed/ethercis-server


## Loading and Running the EtherCIS Server Container

This container is best run on a Linux platform or Virtual Machine, eg Ubuntu 18.04

1) Install Docker (unless already installed)

        curl -sSL https://get.docker.com | sh

To avoid using *sudo* when running *docker* commands:

        sudo usermod -aG docker ${USER}
        su - ${USER}

  NB: You'll be asked to enter your Linux password


2) Load the Container

        docker pull rtweed/ethercis-server


3) Create a Docker Network (unless already created)

        docker network create ecis-net

Confirm that it's been created by listing your Docker networks

        docker network ls

You should see ecis-net included in the list as a *bridged* network


3) Running the Container

        docker run -it --rm --name ethercis-server --net ecis-net -e DB_IP=ethercis-db -e DB_PORT=5432 -e DB_USER=postgres -e DB_PW=postgres -p 8081:8080 rtweed/ethercis-server

Notes:

- the DB_IP environment variable value should match the name you specified in the *docker run* command
  that started the EtherCIS database Container

- the DB_PORT, DB_USER and DB_PW values should be left as specified above

- change the external listener port as required.  In the example above, it will be listening on
  port 8081.  The intername listener port **MUST** be 8080


Leave the EtherCIS server a few seconds to start up.  It should then be connecting to the
EtherCIS Database Container and is ready for use.


## Acknowledgements
* much of the original work for this repo came from https://github.com/inidus/ethercis-docker by [Seref Arikan](https://github.com/serefarikan)
* also helpful was this other EtherCIS docker setup https://github.com/alessfg/docker-ethercis
