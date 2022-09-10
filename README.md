# Ansible Role: contojo.netbox

Ansible role that deploys and configures [Netbox](https://docs.netbox.dev/en/stable/), an IP address management (IPAM) and data center infrastructure management (DCIM) tool.

**Note:** This role will deploy NetBox within its own Python virtualenv using uWSGI as the application server running under systemd which is a little different to the official install docs.


## Supported Platforms

| OS Family | Distribution  | Latest | Supported Version(s) | Comment |
|-----------|---------------|--------|----------------------|---------|
| Debian    | Debian        | :x: | 10 | |
| Debian    | Debian        | :heavy_check_mark: | 11 | |
| Debian    | Ubuntu        | :heavy_check_mark: | 22.04 | |

## Requirements

Ansible Core 2.11 or higher.

## Variables

See [defaults/main.yml](defaults/main.yml) for all variables and their defaults.

## Dependencies

None.

## Example Playbook

This builds an all-in-one instance of Netbox, runs migrations and creates an
admin account - `admin/admin`

```yaml
---

- hosts: all
  become: true
  gather_facts: true
  roles:
    - { role: geerlingguy.postgresql }
    - { role: geerlingguy.redis }
    - { role: geerlingguy.nginx }
    - { role: contojo.netbox }
  vars:
    netbox_greenfields_install: true
    netbox_stable_version: 3.3.0

    postgres_users_no_log: false
    postgresql_users:
      - name: netbox
        password: netbox

    postgresql_databases:
      - name: netbox
        owner: netbox

    nginx_listen_ipv6: false
    nginx_remove_default_vhost: true
    nginx_service_state: started
    nginx_service_enabled: true

    nginx_vhosts:
      - listen: "80 default_server"
        server_name: "_"
        return: "301 https://$host$request_uri"
        filename: "netbox.80.conf"
      - listen: "443 ssl http2"
        server_name: "_"
        filename: "netbox.443.conf"
        extra_parameters: |
          client_max_body_size 25m;
          location = /favicon.ico { access_log off; log_not_found off; }
          location /static/ {
            alias /srv/netbox/current/netbox/static/;
          }
          location / {
            proxy_pass http://127.0.0.1:8000;
            proxy_set_header Host $http_host;
            proxy_set_header X-Forwarded-Host $http_host;
            proxy_set_header X-Forwarded-For $remote_addr;
            proxy_set_header X-Forwarded-Proto "https";
            proxy_set_header X-HTTP_USER_AGENT $http_user_agent;
            proxy_buffering off;
          }
          ssl_certificate /etc/ssl/certs/ssl-cert-snakeoil.pem;
          ssl_certificate_key /etc/ssl/private/ssl-cert-snakeoil.key;
```

## License and Author

- Author:: [aussielunix](https://gitlab.com/aussielunix/)
- Copyright:: 2022, [Contojo Pty Ltd](https://gitlab.com/aussielunix/)

Licensed under the [MIT License](https://opensource.org/licenses/MIT).
See [LICENSE](https://gitlab.com/aussielunix/ansible/ansible-role-netbox/blob/main/LICENSE) file in repository.
