# Testing Ansible using Docker

In order to test Ansible you can create two Docker containers on your local machine.

The first container will act as an example target server e.g. linux with OpenSSH installed.

The second container will be used to do your Ansible testing e.g. run ad-hoc commands and test playbooks. 

These two containers can be built using the Dockerfiles provided (in the "**/ubuntu-openssh/**" and "**/ubuntu-ansible/**" directories).

For convenience there are also two public automated builds of these images hosted on Docker Hub, which can be pulled from my account.

## Using the images on Docker hub

You can pull down the latest "**ubuntu-openssh**" image from my account as follows:

```docker pull robertbarrow/ubuntu-openssh```

e.g.

```
$ docker pull robertbarrow/ubuntu-openssh
Using default tag: latest
latest: Pulling from robertbarrow/ubuntu-openssh
a48c500ed24e: Already exists
1e1de00ff7e1: Already exists
0330ca45a200: Already exists
471db38bcfbf: Already exists
0b4aba487617: Already exists
4f6fa4f06ac8: Pull complete
699075078b83: Pull complete
ea75ecdd0cd0: Pull complete
2042dc99ad05: Pull complete
9540183f34e3: Pull complete
3c604ffaa258: Pull complete
Digest: sha256:e5ce8bb1f865a93e86317c5925ca05685fa9be6e163084e0ef10f9671a3904e1
Status: Downloaded newer image for robertbarrow/ubuntu-openssh:latest
```

You can pull down the latest "**ansible**" image from my account as follows:

```docker pull robertbarrow/ansible```

e.g.

```
$ docker pull robertbarrow/ansible
Using default tag: latest
latest: Pulling from robertbarrow/ansible
a48c500ed24e: Already exists
1e1de00ff7e1: Already exists
0330ca45a200: Already exists
471db38bcfbf: Already exists
0b4aba487617: Already exists
d2fb17fa3d79: Pull complete
5e7be7e115b6: Pull complete
ee427dc0889c: Pull complete
1f215fee4d80: Pull complete
Digest: sha256:f6cacdcc1ce18d32833f93744cc5461eb46bc7524965e5acabce839681ef06c5
Status: Downloaded newer image for robertbarrow/ansible:latest
```


