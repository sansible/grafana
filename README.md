# grafana 

Master: [![Build Status](https://travis-ci.org/sansible/grafana.svg?branch=master)](https://travis-ci.org/sansible/grafana)
Develop: [![Build Status](https://travis-ci.org/sansible/grafana.svg?branch=develop)](https://travis-ci.org/sansible/grafana)

* [ansible.cfg](#ansible-cfg)
* [Installation and Dependencies](#installation-and-dependencies)
* [Tags](#tags)
* [Example](#example)

This role installs the Grafana analytics and monitoring platform..

For more information about Grafana please visit
[https://grafana.com/](https://grafana.com/).



## ansible.cfg

This role is designed to work with merge "hash_behaviour". Make sure your ansible.cfg contains these settings

```INI
[defaults]
hash_behaviour = merge
```


## Installation and Dependencies

This role will install `sansible.users_and_groups` for managing `grafana` user.

To install run `ansible-galaxy install sansible.grafana` or add this to your `roles.yml`

```YAML
- name: sansible.grafana
  version: v1.0
```

and run `ansible-galaxy install -p ./roles -r roles.yml`


## Tags

This role uses two tags: **build** and **configure**

* `build` - Installs Grafana Server and all it's dependencies.
* `configure` - Configure and ensures that the Grafana Server service is running.


## Example

Simply include the role in your playbook to accept the defaults:

sqlite3 database backend

When using sqlite3 grafana will automatically start.

```YAML
- name: Install Grafana Server
  hosts: "{{ host }}"

  roles:
    - name: sansible.grafana
```

Include the role in your playbook and override the defaults to connect to another database.
When using use a database backend other than the default sqlite3, grafana will not start automatically. 
It can be started once the database and defined user have been created.

```YAWL
- name: Install and configure the grafana server
  hosts: "{{ host }}"
  
  roles:
    - role: sansible.grafana
      grafana:
        db:
          host: mysqlhost.local
          name: grafana
          password: grafanadbpass
          port: 3306
          type: mysql
          user: grafana
``` 
