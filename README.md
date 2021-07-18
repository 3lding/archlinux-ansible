ArchLinux Workstation
=========

This Ansible Role is used for setting up a working ArchLinux Workstation with encrypted BTRFS and subvolumes.

Requirements
------------

- Ansible >= 2.7
- A machine to setup
- ArchLinux Install USB


Role Variables
--------------

There are several variables pre-defined inside ``default`` and ``vars``. Feel free to customize them for your purposes.

Variables that are needed:

This variables are important and should be stored inside a Ansible Vault file (see Setup for further information).

```yaml
---
# Example data
vault_luks_pass: 'myDriveToEncrypt!'
vault_users:
   arch:
      password: 'someGreatPassword!'
```

Setup
--------------

1. Write the latest ArchLinux ISO on a USB drive
2. Insert the USB drive into your machine that you want to setup
3. Boot from USB
4. Ensure that Ansible is able to connect to your machine (SSH Authorized Keys)
5. Prepare your inventory 

```
# For example 
inventory/
   provision/
      group_vars/
         arch/
```
6. Edit variables for your needs
7. Create Ansible Vault file (like in the example above inside the ``group_vars`` with name ``vault``) with required secrets for LUKS and your users you want to create on your new machine

```sh
# Create and edit new vault file 
ansible-vault create /inventory/provision/group_vars/arch/vault
# Edit vault file
ansible-vault edit /inventory/provision/group_vars/arch/vault
```

8. Test connection

```sh
ansible <inventory_host> -m ping
```
9. Store vault password into a file so that Ansible is able to decrypt your previous defined secrets
10. Run the playbook

```sh
ansible-playbook play.yml --vault-password-file /path/to/vault/password/file
```


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: myworkstation
      roles:
         - archlinux-ansible

License
-------

BSD 3 Clause

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
