## Dive Into Ansible Course Lab

Lab configuration for DiveInto.com's 'Dive Into Ansible' course

The related code repository is available at - https://github.com/spurin/diveintoansible

This is an experimental branch for use with Podman and Podman-Compose.  Support is not guaranteed and your mileage may vary.  Requires root access (owing to the requirements for rootfull connectivity).

### Download and Preparation

With both podman and podman-compose installed, clone the repository -

```git clone --branch podman-compose https://github.com/spurin/diveintoansible-lab.git```

### Create the user home directories

Unlike docker-compose, podman-compose doesn't auto create the user home directories during startup.  It is important that these are empty so that
they are populated as the user is added, during first initialization.  Run the following command -

```
for entry in 1 2 3 4 5 6 -c; do for os in centos ubuntu; do mkdir -p ansible_home/${os}${entry}/ansible; mkdir -p ansible_home/${os}${entry}/root; done; done
```

### Install the dnsname cni driver

For podman to work with dns resolution, a cni driver of https://github.com/containers/dnsname is required.

This can be downloaded and compiled using golang, alternatively, a precompiled binary is available in the cni folder.  

As root, copy this file to /usr/libexec/cni -

```sudo cp cni/dnsname /usr/libexec/cni/```

### Create a diveinto.io network

```sudo podman network create diveinto.io```

### Update the file /etc/cni/net.d/diveinto.io.conflist

Add the following, to the plugins array -

```
      {
         "type": "dnsname",
         "domainName": "dns.podman",
         "capabilities": {
            "aliases": true
         }
      }
```

As this is json, remember to add the comma to the entry presceding this.  After this is edited, it should look like the following at the bottom of the file -

```
      {
         "type": "firewall",
         "backend": ""
      },
      {
         "type": "tuning"
      },
      {
         "type": "dnsname",
         "domainName": "dns.podman",
         "capabilities": {
            "aliases": true
         }
      }
   ]
}
```

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

Thanks and Kudos to the following for their efforts on this specific use case - [@MaximUltimatum](https://github.com/MaximUltimatum)

![DiveIntoAnsible Cover](DiveIntoAnsible_Cover.png?raw=true "Dive Into Ansible")
