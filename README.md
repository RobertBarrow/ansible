# Testing Ansible using Docker

You can test Ansible using Docker containers on your local machine.

First you'll need at least one container acting as a target server e.g. linux with OpenSSH installed.

Secondly you will need another container running Ansible, which will be used to do your testing e.g. run ad-hoc commands and test playbooks. 

The images required to create these containers can be built using the Dockerfiles provided (in the "**/ubuntu-openssh/**" and "**/ubuntu-ansible/**" directories).

For convenience there are also two public automated builds of these images hosted on Docker Hub, which can be pulled from my account.


## Using the images on Docker hub

To create one or more containers running Ubuntu linux (with OpenSSH installed), you can pull down the latest "**ubuntu-openssh**" image from my account as follows:

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

To create a container with Ansible installed, you can pull down the latest "**ansible**" image from my account as follows:

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
*Note: to keep things simple, this image is also running Ubuntu linux.*

Now that you have the images, you can create your containers as follows...


## Creating Docker containers from the images

To create a detached container running Ubuntu linux with OpenSSH installed:

```docker run -d --name ubuntu-server-1 robertbarrow/ubuntu-openssh```

e.g.

```
$ docker run -d --name ubuntu-server-1 robertbarrow/ubuntu-openssh
7e928a0774403d92b616b1280527bbf98241557f3c2c4a1f01c3f225396a4825
```

*Note: the string that gets returned is the **full** Container ID*

To create an interactive container running Ubuntu linux with Ansible installed:

```docker run -it --rm robertbarrow/ansible```

e.g.

```
$ docker run -it --rm robertbarrow/ansible
root@aad4dfb5aadf:/# ansible --version
ansible 2.5.3
  config file = None
  configured module search path = [u'/root/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/local/lib/python2.7/dist-packages/ansible
  executable location = /usr/local/bin/ansible
  python version = 2.7.15rc1 (default, Apr 15 2018, 21:51:34) [GCC 7.3.0]
root@aad4dfb5aadf:/# exit
exit
```

*Note: the -**it** option provides you with the interactive prompt (via a psuedo TTY session) and the --**rm** option tells the Docker daemon to decompose the container [i.e. shut it down and remove it] once you've exited your interactive session.*


## To see which containers are still running

The ```docker ps``` command will list the containers that you currently have running e.g.

```
$ docker ps
CONTAINER ID        IMAGE                         COMMAND               CREATED             STATUS              PORTS               NAMES
7e928a077440        robertbarrow/ubuntu-openssh   "/usr/sbin/sshd -D"   2 minutes ago       Up 2 minutes       22/tcp              ubuntu-server-1
```

The **ubuntu-openssh** containers are detached, but still actively running the OpenSSH service [listening on port 22].

Adding the "**-a**" option (i.e. ```docker ps -a```) will also list any stopped containers e.g.

```
$ docker ps -a
CONTAINER ID        IMAGE                         COMMAND                  CREATED             STATUS                     PORTS                    NAMES
7e928a077440        robertbarrow/ubuntu-openssh   "/usr/sbin/sshd -D"      17 minutes ago      Up 17 minutes              22/tcp                   ubuntu-server-1
08d93e2796a6        tuned/python-35-rhel7         "container-entrypoint"   7 days ago          Exited (255) 3 hours ago   0.0.0.0:8080->8080/tcp   naughty_galileo
```

As you can see, the **ansible** container is still not listed.  This is due to the "**--rm**" option that was used, which deleted the container after you exited from the interactive prompt.   The ephemeral nature of the **ansible** container means that it would only ever be listed by the ```docker ps``` command if; (**A**) you ran it from another session [whilst you were still at the interactive prompt], or (**B**) if you ran the command as soon as you exited the container and the Docker daemon hadn't finished decomposing it.

