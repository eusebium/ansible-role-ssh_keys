SSH Keys
=========

This role configures all hosts in the current play to allow password-free
(pubkey based) SSH authentication amongst themselves.

Requirements
------------

Ansible 2.8 or higher
OpenSSH software present.

Role Variables
--------------

Available variables can be found in [vars](defaults/main.yml).

Key variables are:
* `ssh_keys_keypair_name` - Name of keypair. This file should NOT be
  the current user's normal private key, unless that key is not considered a secure secret.
* `ssh_keys_keypair_owner` - SSH client user
* `ssh_keys_authorized_keys_owner` - SSH server user

Dependencies
------------

None

Example Playbook
----------------

Example for Production:

```
- hosts: all
  roles:
    - role: eusebium.ssh_keys
      ssh_keys_keypair_name: id_rsa_pgpool
      ssh_keys_keypair_owner: postgres
      ssh_keys_authorized_keys_owner: postgres
```

Example for test/dev:

```
- hosts: all
  roles:
    - role: eusebium.ssh_keys
      ssh_keys_keypair_name: id_test_{{ ssh_keys_keypair_type }}
      ssh_keys_generate_on_controller: true
      ssh_keys_keypair_owner: vagrant
      ssh_keys_authorized_keys_owner: vagrant
      ssh_keys_keypair_comment: 'vagrant_test_key'
```

License
-------

MIT

Author Information
------------------

Sebi C. <cristeaeusebiu@gmail.com>
