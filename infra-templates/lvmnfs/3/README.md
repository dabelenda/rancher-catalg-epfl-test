Rancher-Storage NFSLVM Driver Template
======================================

This repository contains a Rancher Template used in [the EPFL rancher-catalog](https://github.com/epfl-idevelop/rancher-catalog).

This template runs multiple services:

 - [a REST and LVM Server](https://github.com/epfl-idevelop/container-nfslvm-server)
 - [a rancher-storage driver](https://github.com/epfl-idevelop/container-rancher-storage-lvmnfs)

The two in conjunction are used to provide a persistent storage for containers. This storage has the following properties:
 - Strict Quota for each volume, each volume is in its own Logical Volume
 - NFS communications are secure as long as Rancher uses a secure Network Overlay (by default IPSec)

## Requirements

For the driver to work as expected, a *single* rancher host must have the `storage=true` tag. If more than one has this tag behavious of the driver is not defined.

The Docker image of the [Driver](https://github.com/epfl-idevelop/rancher-template-lvmnfs) must have been built using the following procedure:
 - Type `make` so that all the rancher-storage driver images are automatically built
 - `docker tag $(docker images -q rancher/storage-lvmnfs) epflidevelop/storage-lvmnfs` will tag the image using the correct name
 - `docker push epflidevelop/storage-lvmnfs` will upload the image to the docker-hub (if the credentials were given using `docker login`)
