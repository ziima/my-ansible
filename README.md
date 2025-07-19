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
    files:
     - cacert.pem
     - tls_auth
     - kryten-key.pem
     - kryten-cert.pem
```

Put files directly in `playbooks/files` directory.

### Window manager ###
Set window manager using `window_manager`.
Options are `i3` (default) and `xfce4`.

## Manuals for computers setup
### Boot to shell (onetime)
In grub menu press ``e`` to open editor to modify grub commands.
Find row starting with ``linux``.
Append ``init=/bin/bash`` to the end.
Press ``Ctrl+x`` to boot.
Grub will boot to (decrypted) filesystem with only ``/`` mounted readonly. Other partitions shouldn't be mounted.

### Resize partitions
``lvresize`` requires ``/`` partition to be read-write (to write into ``/etc/lvm/archive``).
To remount read-only ``/`` use ``mount -o remount,rw /``.
Follow instruction about resizing partitions on Arch wiki.
To resize ``swap`` partition, use ``mkswap /dev/${VOLUME_GROUP}/${SWAP_PARTITION}``.
