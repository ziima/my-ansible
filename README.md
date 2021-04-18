# my-ansible #
My workstation configuration in ansible.

## Usage ##

1. Install `ansible` and `python-apt`.
2. Check actions:

```sh
ansible-playbook -i hosts/localhost.yml --diff playbooks/home.yml --ask-become-pass --check
```

3. Run ansible:

```sh
ansible-playbook -i hosts/localhost.yml --diff playbooks/home.yml --ask-become-pass
```

## Customization ##
Use `hosts/host_vars/localhost.yml` to customize variables for a local station.
Put custom files, such as openvpn configuration, to `playbooks/files`.

### Users ###
Set users in `host_vars`:

```yaml
users:
  kryten:
    password: "$HASHED$PASSWORD"
    groups:
      - adm  # Read logs
      - bumblebee  # Nvidia switch
      - docker  # Acess to docker
```

### OpenVPN ###
Set openVPN in `host_vars`:

```yaml
openvpn:
  red_dwarf:
    config: red_dwarf.conf
    ca: cacert.pem
    tls_auth: tls_auth
    key: kryten-key.pem
    cert: kryten-cert.pem
```

Put files directly in `playbooks/files` directory.

### Window manager ###
Set window manager using `window_manager`.
Options are `i3` (default) and `xfce4`.
