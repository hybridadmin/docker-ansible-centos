# Centos Docker Images with ansible and systemd

> Centos Docker images to be used for testing ansible playbooks and roles.

## Supported tags and respective `Dockerfile` links

- [`latest`, `8` (*8/Dockerfile*)](https://github.com/hybridadmin/docker-centos-ansible/tree/main/8/Dockerfile)
- [`7` (*7/Dockerfile*)](https://github.com/hybridadmin/docker-centos-ansible/tree/main/7/Dockerfile)

## How to Build the image

1. Install docker
   * [Linux](https://docs.docker.com/engine/install/)
   * [Windows](https://docs.docker.com/docker-for-windows/install/)
2. Clone the repo `git clone https://github.com/hybridadmin/docker-centos-ansible.git`
3. `cd` into the directory
4. Run `docker build -t centos-ansible .`

## How to use this image

Pull the image using the following command:
```console
docker pull hybridadmin/centos-ansible:latest
```

Run a container using the image with the following command:
```console
docker run -d --name systemd-ubuntu --privileged -v /sys/fs/cgroup:/sys/fs/cgroup:ro hybridadmin/centos-ansible:latest
```

Use Ansible inside the container:
```console
docker exec --tty [container_id] env TERM=xterm ansible --version
docker exec --tty [container_id] env TERM=xterm ansible-playbook /path/to/ansible/playbook.yml --syntax-check
```

## Author

Created by Hybridadmin
