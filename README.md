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
- Add sites with several playbooks
- Explicitly remove sites
- Each site can have separate template


## Limitations
- only Debian and Ubuntu
- no SSL (we confifuring SSL on nginx)

Issues welcome!


## Usage

Before this role you must install apache with geerlingguy.apache role or other way.

Some variables names and values matches geerlingguy's role (see default and vars directories). So, you can don't define it twice.

### Add sites:

Site definition matches close too:

```yaml
apache_vhosts_sites:
  www.local.dev:
    servername: "www.local.dev"
    serveralias: "local.dev"
    documentroot: "/var/www/html"
    extra_parameters: |
      RewriteCond %{HTTP_HOST} !^www\. [NC]
      RewriteRule ^(.*)$ http://www.%{HTTP_HOST}%{REQUEST_URI} [R=301,L]
```

Compared with geerlingguy's:

```yaml
apache_vhosts_sites:
  - servername: "www.local.dev"
    serveralias: "local.dev"
    documentroot: "/var/www/html"
    extra_parameters: |
      RewriteCond %{HTTP_HOST} !^www\. [NC]
      RewriteRule ^(.*)$ http://www.%{HTTP_HOST}%{REQUEST_URI} [R=301,L]
```

#### Custom template for site:

```yaml
apache_vhosts_sites:
  www.local.dev:
    servername: "www.local.dev"
    template: "custom.conf.j2"
```

### Remove sites:

```yaml
apache_vhosts_remove_sites:
  - www.local.dev
```


## Example Playbook

```yaml
- hosts: all
  roles:
    - viasite-ansible.apache-vhosts
  vars:
    apache_vhosts_sites:
      foo:
        servername: "local.dev"
        documentroot: "/var/www/html"
      bar:
        servername: "local2.dev"
        documentroot: "/var/www/html"
      templated_site:
        template: tests/custom_template.conf.j2
        servername: "other.dev"
        somevariable: "somevalue"
    apache_vhosts_remove_sites:
      - baz
```
