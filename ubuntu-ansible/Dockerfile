FROM ubuntu:latest

RUN apt update && apt install -y python python-pip sshpass
RUN pip install ansible
RUN mkdir /etc/ansible/
RUN echo '[local]\nlocalhost\n' > /etc/ansible/hosts

EXPOSE 22
CMD ["/bin/bash"]
