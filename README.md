# Simple Rancher UI with support for balanced MySQL and SSL termination out fo rancher config

## Needed files
- PEM certificate for SSL termination for Rancher UI access
- CA file for UI
- PEM certificate for stunnel termination

## Needed parameters:

```
DB_HOST: {{ db_host }}
DB_PORT: {{ db_port }}
DB_NAME: {{ db_name }}
DB_USER_NAME: {{ db_user_name }}
DB_USER_PWD: {{ db_user_pwd }}
CERTS: {{ etc }}/certs
UIIP: {{ grains['fqdn_ip4']|first }}
```

## Haproxy
- you need to setup secondary UI server
- you need to setup IP of mysql hosts

## Stunnel
- expects stunnel running on mysql nodes on port 3307

```
cert = /etc/stunnel/cert.pem
key  = /etc/stunnel/cert.key

chroot = /var/tmp/stunnel
pid = /stunnel.pid

setuid = stunnel
setgid = stunnel
client = no

[mysql]
accept = 3307
connect = 3306
```

# ToDo
- use consul + consulate to populate static host definition
