ansible-role-zabbix_agent
====

Install and configure Zabbix agent. Firewall and yum repository configuration is not part of this role. Check section `Dependencies` for example roles which you can use. 

Requirements
------------

* Zabbix 5.4+
* RHEL8
* YUM repository with zabbix-agent package

Role Variables
--------------

* `zabbix_agent_packages` - list of zabbix packages to install
* `zabbix_agent_config_path` - path to mail zabbix agent config file
* `zabbix_agent_config_d_path` - path to zabbix agent.d config directory
* `zabbix_agent_config` - list of settings for zabbix_agentd.conf, example:

```yaml
zabbix_agent_config:
  - option: Server
    value: zabbix-server.example.com
```

* `zabbix_agent_service_name` - name of zabbix agent service

Dependencies
------------

Collections:

* `community.general`

Roles (optional):

* [ansible-role-firewalld](https://github.com/vladi-k/ansible-role-firewalld)
* [ansible-role-repos](https://github.com/vladi-k/ansible-role-repos)

Example Playbook
----------------

```yaml
- hosts: my_servers
  vars:
    repos_from_rpm:
      - https://repo.zabbix.com/zabbix/6.0/rhel/8/x86_64/zabbix-release-6.0-1.el8.noarch.rpm
    firewalld_ports:
      - port: 10050
        protocol: tcp
    zabbix_agent_config:
      - option: Server
        value: zabbix-server.example.com
  roles:
    - ansible-role-firewalld
    - ansible-role-repos
    - ansible-role-zabbix_agent
```

License
-------

GPLv3

Author Information
------------------

Vladimir Vasilev (@vladi-k)
