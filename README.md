# Fedora 27 Ansible Test Image

Fedora 27 Docker container for Ansible playbook and role testing. Everything which follows borrows *extensively* from the wise examples of Jeff Geerling. He is an amazing teacher. Look him up someday.

## Build Instructions

If you want to build this image yourself, you could perform the following steps:

1. [Install Docker](https://docs.docker.com/engine/installation/).  
2. `cd` into this directory
3. Run the following command
```
docker build -t fedora27-ansible .
```

## Usage  

1. [Install Docker](https://docs.docker.com/engine/installation/).  
2. Pull this image from Docker Hub
```
docker pull brentwg/docker-fedora27-ansible:latest
```  
3. Run a container from the image (to test Ansible roles, also add a volume mounted from your current working directory with `--volume=`pwd`:/etc/ansible/roles/role_under_test:ro`)
```
docker run --detach --privileged --volume=/sys/fs/cgroup:/sys/fs/cgroup:ro brentwg/docker-fedora27-ansible:latest /lib/systemd/systemd
```  
4. Use Ansible inside the container
```
docker exec --tty [container_id] env TERM=xterm ansible --version
```  
&nbsp;&nbsp;&nbsp;&nbsp; or 
```
docker exec --tty [container_id] env TERM=xterm ansible-playbook /path/to/ansible/playbook.yml --syntax-check
```  

## Notes
Follow the example of Jeff Geerling, I use Docker to test Ansible playbooks on multiple OSes using CI tools such as Travis and Jenkins. This container provides provides the capability to test roles and playbooks using Ansible - which runs inside the container.  

> **Disclaimer**: Not intended for use in genuine production environments. I use this for purely development/test/amusement purposes.