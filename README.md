# Ansible Role: ONLYOFFICE DocSpace
Installs and configures ONLYOFFICE DocSpace on Debian/Ubuntu and RedHat servers
#
## Requirements

Role requires nginx, nodejs 12, MYSQL-server, Elasticsearch 7.16, OpenResty, ONLYOFFICE DocumentServer in the system or network. Also this role requires root access, so either run it in a playbook with a global `become: yes`, or invoke the role in your playbook like

    - hosts: your_hosts 
      become: yes
      roles:
        - role: ONLYOFFICE.docspace

## Role Variables

Available variables are listed below, along with default values (see 'defaults/main.yml'):

	db_host: "localhost"

The IP address or the name of the host where the Mysql-server is running.

	db_user: "onlyoffice"

User name for database initialization.

	db_pass: "P@ssw0rd"

User password for connecting to the database.

	db_name: "onlyoffice"

Database name.

## Example playbook with ONLYOFFICE.docspace on a single host

    ---
    - name: Converge
      hosts: 127.0.0.1

      vars:
        ds_port: "8083"
        elasticsearch_package: "{{ 'elasticsearch-7.16.3-1' if ansible_os_family == 'RedHat' else 'elasticsearch=7.16.3' }}"
        postgresql_databases:
          - name: onlyoffice
        postgresql_users:
          - name: onlyoffice
            password: onlyoffice
        erlang_version: 25.3.2.9

    roles:
        - geerlingguy.nodejs
        - ONLYOFFICE.rabbitmq
        - geerlingguy.elasticsearch
        - geerlingguy.postgresql
        - ONLYOFFICE.documentserver
        - ONLYOFFICE.docspace

## License

GNU AGPL v3.0

## Author Information

This role was created by [ONLYOFFICE](https://www.onlyoffice.com/).
