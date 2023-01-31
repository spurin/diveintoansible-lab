## Dive Into Ansible Test Branch

This branch is used for unit testing of Dive Into Ansible.  Upon execution, ubuntu-c will start executing unit tests across the infrastucture that includes -

* .env configuration file access
* volume mounts
* ping connectivity
* sshd connectivity checks
* web terminal connectivity checks
* portal connectivity checks
* playbook execution (verifies that all playbooks execute without error)
* deprecation notices (deprecation warnings have been modified, causing playbook to fail)

To use this branch, configure the .env file as per below and execute

```
ssh-keygen -f config/guest_ssh -P "" <<< y; cp -rf config/guest_ssh config/root_ssh; cp -rf config/guest_ssh.pub config/root_ssh.pub
docker-compose stop; docker-compose rm --force; docker-compose pull; docker-compose up -d
docker logs --follow ubuntu-c
```

This branch is for testing purposes only and is not meant to be used for following the course

![DiveIntoAnsible Cover](DiveIntoAnsible_Cover.png?raw=true "Dive Into Ansible")
