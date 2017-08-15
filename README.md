# ansible-gluon

Ansible Playbook to build Freifunk gluon images

## Description

This is an Ansible Playbook which can be used to automate the build process for [Freifunk](https://freifunk.net/en/) [gluon](https://github.com/freifunk-gluon) images.

## Instructions

Best start with this [Ansible base](https://github.com/andreasscherbaum/ansible-base) repository and add the _Ansible gluon_ repository as role in the _roles/_ directory.

```
git clone https://github.com/andreasscherbaum/ansible-base Freifunk-gluon
cd Freifunk-gluon
git clone https://github.com/Freifunk-Oberhavel/ansible-gluon.git roles/gluon

```

You can add a new _Makefile_ target:

```
gluon:
ifneq  (,$(wildcard roles/gluon))
	cd roles/gluon && git pull
else
	git clone https://github.com/Freifunk-Oberhavel/ansible-gluon.git roles/gluon
endif

```

And add the new role in _install-host.yml_, after the _common_ role:


```
---

- hosts: all
  become: yes
  roles:
    - common
    - gluon

```


Finally initialize the build host, using:

```
make install
```

This will configure the host, install build prerequisites, checkout or update gluon, checkout or update the site config, and build the images with the target defined in _gluon_target_.


## Configuration

The default values for the build are defined in _defaults/main.yml_, and can be overrided by adding variables in _vars/main.yml_ (the placeholders are
already commented out - just uncomment them and fill in values).
