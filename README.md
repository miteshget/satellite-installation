

Role: satellite-installation
============================

This role installs and configure satellite. Also setup & configure firewalld and it's rules.

Requirements
------------

. All required yum repository should be configure to install satellite packages for the version used.

Role Variables
--------------

* `satellite_version: "Digit"` - (Required) | satellite version
* `satellite_admin: "String"` - (Required) | Satellite admin username
* `satellite_admin_password: "String"` - (Required) - Satellite admin password
* `firewall_services: [List]` - (Default=defaults/main.yml) - List of firewall services to enable
* `firewall_ports: [List]` - (Default=defaults/main.yml) - List of firewall ports to enable
* `satellite_org_set_default: Bool` - (Default=true) - Wheter to create an org as default org, or additional one
* `satellite_enable_rex_on_satellite_host: Bool` - (Default=false) - If to allow remote execution jobs to be run against the satellite host (adds a rex key to do that).


* Example variables

```
satellite_version: 6.7
satellite_admin: admin
satellite_admin_password: password
firewall_services:
  - ssh
  - RH-Satellite-6
firewall_ports:
  - 22/tcp
  - 80/tcp
  - 443/tcp
```
Tags
---


|{tag1} |Consistent tag for all satellite install tasks
|{tag2} |For firewall tasks
|{tag3} |For host update tasks
|{tag4} |For satellite setup tasks


* Example tags

```
## Tagged jobs
ansible-playbook playbook.yml --tags install_satellite

## Skip tagged jobs
ansible-playbook playbook.yml --skip-tags install_satellite
```


Example Playbook
----------------

How to use your role (for instance, with variables passed in playbook).
```
[user@desktop ~]$ cat sample_vars.yml
satellite_version: 6.7
satellite_admin: 'admin'
satellite_admin_password: 'changeme'
firewall_services:
  - ssh
  - RH-Satellite-6
firewall_ports:
  - 22/tcp
  - 80/tcp
  - 443/tcp

[user@desktop ~]$ cat playbook.yml
- hosts: satellite.example.com
  vars_files:
    - sample_vars.yml
  roles:
    - satellite-public-hostname
    - satellite-install

[user@desktop ~]$ ansible-playbook playbook.yml -e 'satellite_admin: admin' -e 'satellite_admin_password: password'
```


Author Information
------------------

Mitesh The Mouse <mitsharm@redhat.com>
