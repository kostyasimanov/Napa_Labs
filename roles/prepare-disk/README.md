Prepare Disk Role
=========

This is an Ansible role for prepare disks on Ubuntu system.

Requirements
------------

This role requires Ansible 2.4 or later and has been tested on Ubuntu 22.04.

Role Variables
--------------

The following variables can be customized in this role:

- disk_device: Device like /dev/sda, /dev/sdb, etc. Can be prompted while playbook execution.
- filesystem_type: Filesystem typo, like ext4, xfs, zfs, etc. Can be prompted while playbook execution.
- mount_point: Nothing to say here. Mount point.

Example Playbook
----------------

Here is an example playbook that uses this role:

```yaml
- hosts: servers
  vars_prompt:
    - name: disk_device
      prompt: "Enter disk device (/dev/sda for example)"
      private: false
    - name: filesystem_type
      prompt: "Enter type of filesystem (ext4 for example)"
      private: false

  roles:
    - prepare-disk
```

This playbook prepare your disks on system.

License
----------------
MIT

Author Information
----------------
This role was created by [kostyasimanov](https://gitlab.rebrainme.com/kostyasimanov_at_gmail_com).
