# ansible-initial-setup

My custom Ansible role for initial setup of servers based on Debian. Ensures reasonable defaults for secure SSH login, sets up UFW and Fail2Ban, provides foundation for integrating with Cloudflare and more.

Tested on Debian 10 and Raspberry Pi OS Buster.

## Sample host configuration

```
---
fqdn: samplehost.tld
hostname: samplehost
host_role: nginx_webserver
ssh_port: 2222
deploy_user: user_name_here
cache_valid_time: 3600
authorized_key_file: 'public_keys/user_key_here'
banner_file: etc/issue.net
default_hostname: debian.example.com
ufw_rules_all:
  - { port: 80, proto: any, comment: 'HTTP' }
  - { port: 443, proto: any, comment: 'HTTPS' }
fail2ban: {
  ignoreip: "{{ ssh_allowed_ip }}",
  bantime: 3600,
  findtime: 1800,
  maxretry: 3,
  sender: "fail2ban@example.org",
  destemail: "{{ hostname }}@example.org",
  sendername: "Fail2Ban @ {{ fqdn }}",
}
letsencrypt_email: "email.here@example.org"
```

## License

Licensed under MIT License. See [LICENSE](https://github.com/lwojcik/ansible-initial-setup/blob/master/LICENSE) for more information.
