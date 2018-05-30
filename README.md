# Testing Ansible using Docker

In order to test Ansible you can create two Docker containers on your local machine.

The first container will act as an example target server e.g. running Ubuntu linux with OpenSSH installed.

The second container will be used to do your Ansible testing e.g. run ad-hoc commands and test playbooks. 

These two containers can be built using the Dockerfiles provided (in the "/ubuntu-openssh/" and "/ubuntu-ansible/" directories).

For convenience there are also two public automated builds of these images hosted on Docker Hub, which can be pulled from my account:

```docker pull robertbarrow/ubuntu-openssh```
```docker pull robertbarrow/ansible```


