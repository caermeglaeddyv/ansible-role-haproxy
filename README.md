Ansible role: HAProxy
=========

This role is used to install haproxy by building it from source code.

For now, it does the following:
- downloads lua and haproxy source files to localhost
- downloads build dependencies
- does all necessary preparations in OS
- builds lua
- builds haproxy and configures it
- deletes build files and dependencies


Requirements
------------

This is not strict requirements and it may not work with other versions than tested ones.
Anyway. feel free to test by yourself, suggest addition of new functionality and contribute.

Role is tested with:
- Ansible version >= 2.8.6
- CentOS version >= 7.6 (1803)


Role Variables
--------------

Variables and their descriptions copied from defaults/main.yml

```bash

# HAProxy source files version to download and build from:
haproxy_version: 2.0.9

# Lua source files version to download and build from:
haproxy_lua_version: 5.3.5

# If HAProxy frontend will bind to non-local IP address (like virtual IP
# which floats between servers), this will configure sysctl to allow that:
haproxy_nonlocal_bind: false

# Size of DH parameters file which will be generated to harden TLS connections:
haproxy_dhparam_size: 2048

# Default bind options for TLS:
haproxy_ssl_default_bind_options: ssl-min-ver TLSv1.2

# Default bind ciphers for TLS:
haproxy_ssl_default_bind_ciphers: ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384

# Default server options for TLS:
haproxy_ssl_default_server_options: ssl-min-ver TLSv1.2

# Default server ciphers for TLS:
haproxy_ssl_default_server_ciphers: ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384

# Enable Stats frontend which generates Prometheus-style metrics for monitoring:
haproxy_metrics_prometheus: false

# Name of the frontend:
haproxy_frontend_name: frontend

# Hostname of IP to bind frontend on:
haproxy_frontend_host: ""

# Hostname of IP to bind frontend on:
haproxy_frontend_port:

# Name of the backend:
haproxy_backend_name: backend

# Default server options for the backend:
haproxy_backend_default_server: ""

# Array of backend servers' dns names or IP addresses:
haproxy_backend_servers: []
# - abc.xyz
# - 1.2.3.4

# Port on which backend servers listen:
haproxy_backend_servers_port: 

```


Dependencies
------------

none


Example Playbook
----------------

```bash
---
- hosts: localhost
  gather_facts: false
  become: no
  tasks:
  - name: Check ansible version >=2.8.6
    assert:
      msg: Ansible must be v2.8.6 or higher
      that:
      - ansible_version.string is version("2.8.6", ">=")
    tags:
    - check
  vars:
    ansible_connection: local

- hosts: all
  become: yes
  tasks:
  - import_role:
      name: keepalived

```

More detailed examples ( inventories, playbooks etc. ) of this and other roles can be found [here](https://github.com/caermeglaeddyv/examples/tree/dev/ansible).

It's highly recommended to start you test deploys from there, especially if you use Google Cloud Platform or VMware vCenter as your infrastructure, for now that [repository](https://github.com/caermeglaeddyv/examples) contains [Packer](https://github.com/caermeglaeddyv/examples/tree/dev/packer) and [Terraform](https://github.com/caermeglaeddyv/examples/tree/dev/terraform) examples to build templates and deploy machines on this platforms.


License
-------

[Apache 2.0](https://github.com/caermeglaeddyv/ansible-role-haproxy/blob/dev/LICENSE)


Author Information
------------------

Copyright 2020 [caermeglaeddyv](https://github.com/caermeglaeddyv)
