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
        linux_ad_auth_domain_controller: dc01.acme.com
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

To run test you must pass in the command line the variable `linux_ad_auth_tests_host` pointing to a linux system to use to test the role.

Additionally the tests requires the following set of variables that can be defined in the inventory or passed in the command line:

- `linux_ad_auth_tests_domain_controller`: windows domain controller
- `linux_ad_auth_tests_host_netbios_name`: netbios name to use for the host
- `linux_ad_auth_tests_sssd_simple_allow_groups`: windows group you want to allow to autenticate on the host
- `linux_ad_auth_tests_host_ou`: OU where to put the computer object within active directory
- `linux_ad_auth_tests_user`: windows user to connect
- `linux_ad_auth_tests_password`: password for the previous user
- `linux_ad_auth_tests_intermediate`: windows host fullfilling the ansible requirements documented in https://docs.ansible.com/ansible/latest/user_guide/windows_setup.html. Also, you must define in the inventory for this host the neccessary variables to connect.

One way to provide all the previous information is calling the testing playbook passing the host to use and an additional vault inventory plus the default one provided for testing, as it's show in this example:

```shell
$ cd amtega.linux_ad_auth/tests
$ ansible-playbook main.yml -e "linux_ad_auth_tests_host=test_host" -i inventory -i ~/mycustominventory.yml --vault-id myvault@prompt
```

## License

Copyright (C) 2019 AMTEGA - Xunta de Galicia

This role is free software: you can redistribute it and/or modify it under the terms of:

GNU General Public License version 3, or (at your option) any later version; or the European Union Public License, either Version 1.2 or – as soon they will be approved by the European Commission ­subsequent versions of the EUPL.

This role is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details or European Union Public License for more details.

## Author Information

- Daniel Sánchez Fábregas.
- Juan Antonio Valiño García.
