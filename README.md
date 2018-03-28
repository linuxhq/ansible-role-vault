# ansible-role-vault

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-vault.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-vault)

RHEL/CentOS - A tool for managing secrets

## Requirements

This role requies a storage backend.  By default it's configured
to use consul but supports all storage backends.  Simply update
the dict with the correct options for your backend.

An ansible role for consul can be found here:

 * https://galaxy.ansible.com/linuxhq/consul/

## Role Variables

Available variables are listed below, along with default values:

    vault_backend:
      address: 127.0.0.1:8500
      path: vault
      storage: consul
    vault_bin: /usr/sbin/vault
    vault_config_path: /etc/vault/vault.hcl
    vault_listener:
      address: 127.0.0.1:8200
      tls_disable: 1
    vault_log_file: /var/log/vault/vault.log
    vault_log_level: info
    vault_opts: ''
    vault_pid_file: /var/run/vault/vault.pid
    vault_user: vault

Additional variables available, not defined by default:

    vault_telemetry:
      disable_hostname: true
      statsd_address: 127.0.0.1:8125
      statsite_address: 127.0.0.1:8125

## Dependencies

 * https://galaxy.ansible.com/linuxhq/linuxhq/

## Example Playbooks

Example playbook with a consul storage backend:

    - hosts: servers
      roles:
        - role: linuxhq.vault
          vault_backend:
            address: 127.0.0.1:8500
            path: vault
            storage: consul
          vault_listener:
            address: "{{ ansible_default_ipv4.address }}:8200"
            tls_disable: 1

Example playbook with a mysql storage backend:

    - hosts: servers
      roles:
        - role: linuxhq.vault
          vault_backend:
            address: 127.0.0.1:3306
            database: vault
            password: vault
            storage: mysql
            table: vault
            username: vault
          vault_listener:
            address: "{{ ansible_default_ipv4.address }}:8200"
            tls_disable: 1

## License

Copyright (C) 2018 Taylor Kimball <tkimball@linuxhq.org>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program. If not, see <http://www.gnu.org/licenses/>. 
