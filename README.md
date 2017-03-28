# Info
- HAProxy terminates SSL requests for Racnher Server (UI)
 - redirect HTTP to HTTPS
- Rebalance between multiple Rancher servers if local instance is down
- Balance over MySQL nodes
- Handle SSL termination between Rancher server and MySQL nodes
- Simplified mysql server maintenance, Rancher server upgrades (well sometimes)

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
- haproxy/haproxy.cfg
  - login/password for haproxy UI admin user
  - you need to setup other UI server(s) instance
  - you need to setup IP of mysql host(s)

## Stunnel
- stunnel/stunnel.conf
  - provides endpoint for MySQL on 3306
  - send encrypted communication to mysql node (expects stunnel server running on mysql node on port 3307)

### Sample config for MySQL node stunnel

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
- use vault for credentials

# Credits
 - Courtney Couch, courtney@moot.it (stunnel container setup)
