Nginx Role
=========

This is an Ansible role for installing and configuring Nginx Mainline on Ubuntu system.

Requirements
------------

This role requires Ansible 2.4 or later and has been tested on Ubuntu 22.04.

Role Variables
--------------

The following variables can be customized in this role:

- nginx_binary_url: Registry URL to binary
- nginx_user: User, which is run nginx proccess by systemd unit
- nginx_conf_dir: Directory with nginx virtualhosts

- nginx_http_port: The HTTP port that Nginx should listen on.
- nginx_virtualhosts: A list of virtual hosts to be configured in Nginx. Each virtual host is defined as a dictionary with the following keys:
  - name: A unique name for the virtual host.
  - server_name: The domain name that should be used to access this virtual host.
  - root: The root directory for the virtual host's files.
  - available: The directory where the Nginx configuration files for available virtual hosts should be stored.
  - enabled: The directory where the Nginx configuration files for enabled virtual hosts should be stored. When a virtual host is enabled, a symlink is created from its configuration file in the available directory to the enabled directory.
- virtualhosts_files: A list of default filenames that should be used for the index file of each virtual host. If any of these files exist in the root directory of a virtual host, it will be used as the default page for that virtual host.

Example Playbook
----------------

Here is an example playbook that uses this role:

```yaml
- hosts: servers
  vars:
    nginx_binary_url: "https://example.com/registry/nginx_1.0.0"
    nginx_user: "nginx"
    nginx_conf_dir: "/etc/nginx"
    nginx_virtualhosts:
      available: /etc/nginx/sites-available
      enabled: /etc/nginx/sites-enabled
      hosts:
        - name: "web-1"
          server_name: "web-1.example.com"
          root: "/var/www/web-1"
        - name: "web-2"
          server_name: "web-2.example.com"
          root: "/var/www/web-2"
    virtualhosts_files: ['index', 'index.html', 'index.htm', 'index.nginx-debian.html']
  roles:
     - nginx
```

This playbook installs Nginx and sets the server name to example.com.

License
----------------
MIT

Author Information
----------------
This role was created by [kostyasimanov](https://gitlab.rebrainme.com/kostyasimanov_at_gmail_com).
