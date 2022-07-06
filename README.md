Ansible Ambari Agent
=========

A simple role for setting up Apache Ambari Agent

Requirements
------------

JAVA
MariaDB / PostgreSQL Database

Role Variables
--------------

The following variables are used by this role and values are defined in defaults/main.yml:

ambari_server_master: master1.habibiz             ## ambari server hostname
ambari_agent_log_dir: /var/log/ambari-agent       ## ambari agent log dir
register_agent: False                             ## enable registration
ambari_agent_no_file: 4096                        ## number of open file for ambari agent

Example Playbook
----------------

Here is an example playbook that can readily wrap this role and still be fairly flexible.  You typically don't need to be this flexible on password source.

- hosts: master01.clemlab.com
  gather_facts: no
  vars_files:
  - vars/external_vars_dev.yml
  - vaults/vault-dev.yml

  roles:
    - role: ambari-server
      tags: ambari_server
      vars:
        ambari_database: "{{ ambari_server_database }}"
        ambari_database_user: "{{ ambari_server_database_user }}"
        ambari_database_user_password: "{{ ambari_server_database_user_password }}"
        ambari_ssl: "{{ ambari_server_ssl }}"
        ambari_ssl_port: "{{ ambari_server_ssl_port }}"
        mysql_server_hostname: "{{ mariadb_server }}"
        mysql_server_port: 3306
        ambari_master_key: "{{ ambari_server_master_key }}"
        ssl_cert_folder: "{{ security_ssl_cert_folder }}"
        ssl_stores_path: "{{ security_server_ssl_stores }}"
        truststore_password: "{{ security_truststore_password }}"
        java_home: /usr/lib/jvm/java

License
-------

GPLv2

Author Information
------------------

https://github.com/lucasbak/
https://github.com/ymadoff/
