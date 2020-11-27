# my-ansible #
My workstation configuration in ansible.

## Usage ##

1. Install `ansible` and `python-apt`.
2. Check actions:

```sh
ansible-playbook -i hosts_localhost --diff playbooks/home.yml --ask-become-pass --check
```

3. Run ansible:

```sh
ansible-playbook -i hosts_localhost --diff playbooks/home.yml --ask-become-pass
```

## Customization ##
Use `host_vars/localhost.yml` to customize variables for a local station.
Put custom files, such as openvpn configuration, to `playbooks/files`.
