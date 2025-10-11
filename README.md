Ansible Role: TT-RSS-docker
===========================

Install Tiny Tiny RSS Docker Compose project.
- https://github.com/tt-rss/tt-rss

Requirements
------------

Requires the following to be installed:
- docker
- docker compose

Role Variables
--------------

Common Docker projects variables:

```yaml
# Base directory for Docker projects
docker_projects_path: # /var/apps
```

Available role variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
# Docker project variables

tt_rss_project_name: tt-rss

tt_rss_traefik_entrypoints: 'http,https'
tt_rss_traefik_middlewares:
  - "https-redirect@file"
```

```yaml
# TT-RSS project variables

# TT-RSS app image source
# tt_rss_app_image: supahgreg/tt-rss
tt_rss_app_image: ghcr.io/tt-rss/tt-rss

# TT-RSS nginx image source
# tt_rss_nginx_image: supahgreg/tt-rss-web-nginx
tt_rss_nginx_image: ghcr.io/tt-rss/tt-rss-web-nginx

# TT-RSS app image version
tt_rss_version: latest
# TT-RSS nginx image version
tt_rss_nginx_version: latest

# postgres image version
tt_rss_postgres_version: 18-alpine

# Set admin user password to this value.
# If not set, random password will be generated on startup, look for it in the 'app' container logs.
# tt_rss_admin_user_pass:

# Sets admin user access level to this value. Valid values:
#   -2 - forbidden to login
#   -1 - readonly
#    0 - default user
#   10 - admin
# tt_rss_admin_user_access_level:

# Database host (defaults to bundled PostgreSQL container)
tt_rss_db_host: db
# Database network (external)
tt_rss_db_network:
# Database credentials
tt_rss_db_user: postgres
tt_rss_db_name: postgres
tt_rss_db_pass: password

# You will likely need to set this to the correct value - it should point to external tt-rss URL as seen in your browser.
tt_rss_self_url_path: https://example.com/tt-rss

# Bind exposed port to 127.0.0.1 to run behind reverse proxy on the same host. If you plan expose the container, remove "127.0.0.1:".
# Leave empty to disable container port binding
tt_rss_http_port: 127.0.0.1:8280

# Optional, makes weekly backups of your install
tt_rss_backups: true
```

Dependencies
------------

This role depends on :
- [djuuu.docker_project](https://github.com/Djuuu/ansible-role-docker-project)

Some variables allow integration with:
- [djuuu.traefik_docker](https://github.com/Djuuu/ansible-role-traefik-docker)

Example Playbook
----------------

```yaml
- hosts: all
  gather_facts: true
  gather_subset:
    - "!all"
    - "!min"
    - user_id

  roles:
    - djuuu.ttrss_docker
```

License
-------

Beerware License
