# Testing Ansible using Docker

In order to test Ansible you can create two Docker containers on your local machine.

The first container will act as an example target server (running Ubuntu linux with OpenSSH installed).
This can be built using the Dockerfile in the /ubuntu-openssh/ directory or just pulled from my account:

```docker pull robertbarrow/ansible```

Note: this is a public automated build image hosted on Docker Hub.

The second container will be used to do your Ansible testing e.g. run ad-hoc commands and test playbooks. 
It is also based on Ubuntu linux and comes with Ansible pre-installed.
This can be built using the Dockerfile in the /ubuntu-ansible/ directory or just pulled from my account:

```docker pull robertbarrow/ubuntu-openssh```

Note: this is a public automated build image hosted on Docker Hub.


