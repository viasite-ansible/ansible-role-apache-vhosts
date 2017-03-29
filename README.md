# Ansible Role: Apache vhosts
[![Build Status](https://travis-ci.org/viasite-ansible/ansible-role-apache-vhosts.svg?branch=master)](https://travis-ci.org/viasite-ansible/ansible-role-apache-vhosts)


## Purpose

I am using role [geerlingguy.apache](https://github.com/geerlingguy/ansible-role-apache) with roles 
[jdauphant.nginx](https://github.com/jdauphant/ansible-role-nginx) and 
[viasite-ansible.site](https://github.com/viasite-ansible/ansible-role-site).

jdauphant.nginx manage sites in separate files and role supporting explicitly remove sites.

Geerlingguy [commented](https://github.com/geerlingguy/ansible-role-apache/issues/94#issuecomment-227237493) purpose of single vhosts.conf.

Role viasite-ansible.site does complex site setup: user creation, setup nginx, apache, mysql etc. Each site plays as separate role,
so I need for separate apache vhosts too.

This role allow of using geerlingguy.apache other way.

Other roles "apache-vhosts" that I found doing same that viasite-ansible.site: it too complex.


## Features
- 


## Limitations
- only Debian and Ubuntu
- no SSL (we confifuring SSL on nginx)

Issues welcome!


## Usage

Before this role you must install apache with geerlingguy.apache role or other way.

### Sample playbook:
```

```
