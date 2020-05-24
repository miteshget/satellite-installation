

Role: satellite-installation
============================

This role installs and configure satellite. Also setup & configure firewalld and it's rules.

Requirements
------------

* Satellite repository or subscription must be pre-configure 
* DNS IP address must be configured, DNS server must have A and PRT records for the host. 

Role Variables
--------------

* `satellite_version: "Digit"`          - (Required) - satellite version
* `satellite_admin: "String"`           - (Required) - Satellite admin username
* `satellite_admin_password: "String"`  - (Required) - Satellite admin password
* `satellite_arguments: [List]` - (Default=defaults/main.yml) - Additional arguments to *`satellite-installation`* command.
* `initial_satellite_org: "String"` - (Default=defaults/main.yml) - Initial satellite organization name.
* `env_type: "String"` - (Required) - directory inside ./configs/{{ env_type }}, which will be used to keep pre & post setup files. 
* `firewall_services: [List]` - (Default=defaults/main.yml) - List of firewall services to enable
* `firewall_ports: [List]` - (Default=defaults/main.yml) - List of firewall ports to enable


Sample variable example 
-----------------------
```
satellite_version: 6.7
satellite_admin: <may be admin>
satellite_admin_password: <somethingstrong>"
firewall_services:
  - ssh
  - RH-Satellite-6
firewall_ports:
  - 22/tcp
  - 80/tcp
  - 443/tcp
```

Pre-satellite installation tasks
--------------------------------
In case, you have some pre satellite package installation tasks then create following file in given path and write your tasks otherwise no need to create this file. Default is ignore if file is not exist. 

* ./configs/{{ env_type }}/satellite_pre_installation.yml


Post-satellite installation tasks
---------------------------------
In case, you have some post satellite package installation tasks then create following file in given path and write your tasks otherwise no need to create this file. Default is ignore if file is not exist.

* ./configs/{{ env_type }}/satellite_post_installation.yml

Pre-satellite configuration tasks
---------------------------------
In case, you have some pre satellite configuration *`(Just before satellite-installation command execution)`* tasks then create following file in given path and write your tasks otherwise no need to create this file. Default is ignore if file is not exist.

* ./configs/{{ env_type }}/satellite_pre_configuration.yml

Post-satellite configuration tasks
---------------------------------
In case, you have some post satellite configuration *`(Just after satellite-installation command execution finishes)`* tasks then create following file in given path and write your tasks otherwise no need to create this file. Default is ignore if file is not exist.

* ./configs/{{ env_type }}/satellite_post_configuration.yml

Tags
----


* *`install_satellite`* - Consistent tag for all satellite install tasks
* *`configure_satellite`* - For satellite setup tasks
* *`install_firewall`* - For firewall tasks




* Example tags

```
## Tagged jobs
[user@node ~]$ ansible-playbook playbook.yml -e @./sample_vars.yml --tags install_satellite

## Skip tagged jobs
[user@node ~]$ ansible-playbook playbook.yml -e @./sample_vars.yml --skip-tags configure_satellite
```


Example Playbook
----------------

How to use the role in playbook and variables are put in sample_vars.yml.

```
[user@node ~]$ cat sample_vars.yml
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

[user@node ~]$ cat playbook.yml
- hosts: satellite.example.com
  roles:
    - satellite-install

[user@node ~]$ ansible-playbook playbook.yml -e @./sample_vars.yml
```
License
-------
GPLv3

Author Information
------------------
Mitesh The Mouse <mitsharm@redhat.com>
