# dovecot

## Description
Ansible role to install an configure dovecot on CentOS.

## Example Playbook
```YAML
---
- name: Dovecot
  hosts: all
  become: true
  gather_facts: true

  roles:
    - role: bubebyte.dovecot
```

## Role Variables
These are the role default which are set in default/main.yml:
```YAML
---
dovecot_extra_packages: []
dovecot_auth_method: system
dovecot_sql_backend: mysql  # relevant only if dovecot_auth_method is set to sql
dovecot_protocols: ""  # if left blank, the systrem default will be used

dovecot_sql_backend_hostname: localhost
dovecot_sql_backend_databasename: maildb
dovecot_sql_backend_user: maildbusr
dovecot_sql_backend_password: "ChangeMePLZ!"
dovecot_sql_password_query: "SELECT username, domain, password FROM users WHERE username = '%Ln' AND domain = '%Ld' AND active = 'Y'"
dovecot_sql_user_query: "SELECT home, uid, gid FROM users WHERE username = '%Ln' AND domain = '%Ld' AND active = 'Y'"

dovecot_ssl_cert_path: /etc/pki/dovecot/certs/dovecot.pem
dovecot_ssl_key_path: /etc/pki/dovecot/private/dovecot.pem

dovecot_mail_location: "maildir:~/Maildir"
dovecot_mail_namespace:
  inbox:
    inbox: "yes"

dovecot_mailboxes_namespace:
  inbox:
    Drafts:
      special_use: \Drafts
    Junk:
      special_use: \Junk
    Trash:
      special_use: \Trash
    Sent:
      special_use: \Sent
    "Sent Messages":
      special_use: \Sent

dovecot_service:
  imap-login:
    inet_listener imap:
      port: 143
    inet_listener imaps:
      port: 993
      ssl: "yes"
    service_count: 1
  pop3-login:
    inet_listener pop3: {}
    inet_listener pop3s: {}
  submission-login:
    inet_listener submission: {}
  lmtp:
    unix_listener lmtp: {}
  imap: {}
  pop3: {}
  submission: {}
  auth:
    unix_listener auth-userdb: {}
  auth-worker: {}
  dict:
    unix_listener dict: {}

dovecot_managesieve: false
dovecot_managesieve_port: 4190
```

## Requirements

### Roles
none

### Collections
none

## License
MIT License

## Author Information
[Armin Bube](https://bubebyte.de)
