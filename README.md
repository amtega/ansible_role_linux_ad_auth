# Ansible linux_ad_auth role

This is an [Ansible](http://www.ansible.com) role which setups system authentication to use Windows Active Directory.

## Role Variables

A list of all the default variables for this role is available in `defaults/main.yml`.

## Example Playbook

```yaml
- name: Sample of sssd role  
  hosts: the-acme-host-for-testing
  tasks:
    - include_role:
        name: amtega.linux_ad_auth
      vars:
        linux_ad_auth_domain: acme.com
        linux_ad_auth_host_netbios_name: tah-for-testing
        linux_ad_auth_sssd_simple_allow_groups:
          - linux-administrator
        linux_ad_auth_host_ou: >-
          OU=Linux,OU=Servers,OU=Resoures,DC=acme,DC=com
        linux_ad_auth_user: admin
        linux_ad_auth_password: password
        linux_ad_auth_state: present
```

## Testing

Tests are based on [molecule with vagrant virtual machines](https://molecule.readthedocs.io/en/latest/installation.html).

To run the the tests you need and inventory with the following set of variables:

- `linux_ad_auth_tests_domain`: windows domain
- `linux_ad_auth_tests_host_netbios_name`: netbios name to use for the host
- `linux_ad_auth_tests_sssd_simple_allow_groups`: windows group you want to allow to autenticate on the host
- `linux_ad_auth_tests_host_ou`: OU where to put the computer object within active directory
- `linux_ad_auth_tests_user`: windows user to connect
- `linux_ad_auth_tests_password`: password for the previous user
- `linux_ad_auth_tests_intermediate`: windows host fullfilling the ansible requirements documented in https://docs.ansible.com/ansible/latest/user_guide/windows_setup.html. Also, you must define in the inventory for this host the neccessary variables to connect.

Additionally, to run test you must setup the following environment variables:

- `LINUX_AD_AUTH_TESTS_HOST`: host to use to test the role.
- `LINUX_AD_AUTH_TESTS_HOST_NETBIOS_NAME`: netbios name to use for the host
- `ANSIBLE_INVENTORY`: path to the inventory
- `ANSIBLE_VAULT_PASSWORD_FILE`: path to the file containing the vault password required for the previous inventory

```shell
cd amtega.linux_ad_auth

LINUX_AD_AUTH_TESTS_HOST=mytestinghost LINUX_AD_AUTH_TESTS_HOST_NETBIOS_NAME=mynetbiosname ANSIBLE_INVENTORY=~/myinventory ANSIBLE_VAULT_PASSWORD_FILE=~/myvaultpassword molecule test --all
```

## License

Copyright (C) 2022 AMTEGA - Xunta de Galicia

This role is free software: you can redistribute it and/or modify it under the terms of:

GNU General Public License version 3, or (at your option) any later version; or the European Union Public License, either Version 1.2 or – as soon they will be approved by the European Commission ­subsequent versions of the EUPL.

This role is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details or European Union Public License for more details.

## Author Information

- Daniel Sánchez Fábregas.
- Juan Antonio Valiño García.
- José Enrique Mourón Regueira.
- PowerShell script based on Brian Scholer (@briantist) work.
