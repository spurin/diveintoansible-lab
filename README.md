## Dive Into Ansible Course Lab

Lab configuration for DiveInto.com's 'Dive Into Ansible' course

The related code repository is available at - https://github.com/spurin/diveintoansible

This is an experimental branch for use with Podman and Podman-Compose.  Support is not guaranteed and your mileage may vary.  Requires root access (owing to the requirements for rootfull connectivity).

### Download and Preparation

With both podman and podman-compose installed, clone the repository -

```git clone --branch podman-compose https://github.com/spurin/diveintoansible-lab.git```

### Install the dnsname cni driver

For podman to work with dns resolution, a cni driver of https://github.com/containers/dnsname is required.

This can be downloaded and compiled using golang, alternatively, a precompiled binary is available in the cni folder.  

As root, copy this file to /usr/local/libexec/cni -

```sudo cp cni/dnsname /usr/local/libexec/cni/```

### Create a diveinto.io network

```sudo podman network create diveinto.io```

Once complete, listing the network should show the PLUGIN of dnsname -

```sudo podman network ls```

### Start the lab

```sudo podman-compose -t identity up```

Unlike the docker-compose equivalent there is no 'Attaching to' statement, once all the containers have started you will see the following -

```
podman start -a ubuntu-c
podman start -a ubuntu1
podman start -a ubuntu2
podman start -a ubuntu3
podman start -a centos1
podman start -a centos2
podman start -a centos3
podman start -a docker
podman start -a portal
```

Keep this terminal open and running whilst using the course.  In your browser, then browse to http://localhost:1000 and you should get the lab interface

### Stopping and removing the lab

```
sudo podman stop --all; sudo podman rm --all
```

### Thanks and Kudos!

Thanks and Kudos to the following for their efforts on this specific use case - @MaximUltimatum

![DiveIntoAnsible Cover](DiveIntoAnsible_Cover.png?raw=true "Dive Into Ansible")
