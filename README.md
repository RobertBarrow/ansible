# Testing Ansible using Docker

In order to test Ansible you can create two Docker containers on your local machine.

The first container will act as a target server (running Ubuntu linux with OpenSSH installed).
This can be built using the Dockerfile in the /ubuntu-openssh/ directory or just pulled from my account:

```docker pull robertbarrow/ansible```

Note: this is a public automated build image hosted on Docker Hub.

The second containser will act as our Ansible administration client (running Ubuntu linux with Ansible installed).
This can be built using the Dockerfile in the /ubuntu-ansible/ directory or just pulled from my account:

```docker pull robertbarrow/ubuntu-openssh```

Note: this is a public automated build image hosted on Docker Hub.


