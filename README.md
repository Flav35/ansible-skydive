Role
=========
Ansible Skydive role (http://skydive-project.github.io/skydive) :
* Install Skydive from sources or use binary
* Create a minimal configuration and systemd unit files for Skydive

Requirements
------------
ansible 2.1

Role Vars
--------------
### Base
```yaml
from_sources: True/False
```
### Skydive service type
```yaml
sd_service_type: agent/analyzer
sd_host: 127.0.0.1
```
### Port binding
```yaml
sd_analyzer_port: 8082
sd_agent_port: 8081
```
### Basic config (see https://github.com/skydive-project/skydive/blob/master/etc/skydive.yml.default)
```yaml
sd_ws_pong_timeout: 5
sd_cache_expire: 300
sd_cache_cleanup: 30
```
### For OpenStack binding
```yaml
os_bind: no
os_auth_url: "http://controller:5000/v2.0"
os_username: "admin"
os_password: "pass123"
os_tenant_name: "admin"
os_region_name: "RegionOne"
```
Dependencies
------------
ansible-go (https://github.com/jlund/ansible-go) if you want to build Skydive from sources


Playbook examples
-------------------
```yaml
    - hosts: computes
      roles:
      - { role: ansible-skydive, sd_service_type: "agent" }
```

```yaml
    - hosts: controller
      roles:
      - ansible-go
      - { role: ansible-skydive, sd_service_type: "analyzer", from_sources: "yes" }
```

Distrib Support
--------------------
| Distribution | Compat | Test  |
| ------------ |:------:| :----:|
|   Centos 7   |   Y    |   Y   |
|   Debian 8   |   Y    |   N   |
