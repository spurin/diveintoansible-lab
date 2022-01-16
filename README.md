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
docker-compose rm; rm -rf ansible_home/tests; docker-compose up
```

This branch is for testing purposes only and is not meant to be used for following the course

![DiveIntoAnsible Cover](DiveIntoAnsible_Cover.png?raw=true "Dive Into Ansible")
