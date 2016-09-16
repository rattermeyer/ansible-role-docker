Role Name
=========
This role installs docker on the managed hosts. It builds upon [angstwad.docker](https://github.com/angstwad/docker.ubuntu) with few changes:

* dropped support for ubuntu 12.04
* allows installation of a specific docker version and installs a package fix (so update does not update version)
* currently no ufw handling

Requirements
------------

Requires python-pycurl for apt modules.

Role Variables
--------------

These are the defaults, which can be set to present to prevent a reboot if the latest linux-image-extra, cgroup-lite packages are already installed. The following role variables are defined:

```
---
# defaults file for ansible-role-docker
# docker-engine is the default package name
docker_pkg_name: docker-engine
docker_pkg_version: latest
docker_apt_cache_valid_time: 600

# docker dns path for docker.io package ( changed at ubuntu 14.04 from docker to docker.io )
docker_defaults_file_path: /etc/default/docker

# Place to get apt repository key
apt_key_url: hkp://p80.pool.sks-keyservers.net:80
# apt repository key signature
apt_key_sig: 58118E89F3A912897C070ADBF76221572C52609D
# Name of the apt repository for docker
apt_repository: deb https://apt.dockerproject.org/repo ubuntu-{{ ansible_distribution_release }} main
# The following help expose a docker port or to add additional options when
# running docker daemon.  The default is to not use any special options.
#docker_opts: >
#  -H unix://
#  -H tcp://0.0.0.0:2375
#  --log-level=debug
docker_opts: ""
# List of users to be added to 'docker' system group (disabled by default)
# SECURITY WARNING:
# Be aware that granted users can easily get full root access on the docker host system!
docker_group_members: []
# Flags for whether to install pip packages
pip_install_pip: true
pip_install_setuptools: true
pip_install_docker_py: true
pip_install_docker_compose: true
# Versions for the python packages that are installed
pip_version_pip: latest
pip_version_setuptools: latest
pip_version_docker_py: latest
pip_version_docker_compose: latest

# Set to 'yes' or 'true' to enable updates (sets 'latest' in apt module, and remove package fix)
# Set to 'no' or 'false' to fix version (sets to the specific docker_version and installs apt package fix)
update_docker_package: no
```

Dependencies
------------

None.

Testing
-------

To test the role in a Vagrant environment just run `vagrant up`.  This will
create one VM based on Ubuntu 14.04,
and it will provision them by applying this role with Ansible.

Requires `ansible-playbook` to be in the path.

License
-------

Apache v2.0
