# bitly OAuth2-proxy ansible role

[![Build Status](https://travis-ci.org/morbidick/ansible-role-oauth2-proxy.svg?branch=master)](https://travis-ci.org/morbidick/ansible-role-oauth2-proxy)

An ansible role to install and configure [oauth2 proxy](https://github.com/bitly/oauth2_proxy).

## Variables

```yaml
oaut2_proxy_http                         : "https://github.com/bitly/oauth2_proxy/releases/download/v2.1/oauth2_proxy-2.1.linux-amd64.go1.6.tar.gz"
oaut2_proxy_http_sha256                  : "3061e5b04bd14eeb9ec0ad1c9b324ba8d99d50eaadc5f528cdf4d21043828298"
oauth2_user                              : "oauth2"
oauth2_dir                               : "/var/oauth2_proxy"
oauth2_dir_tmp                           : "/var/oauth2_proxy/tmp"
oauth2_dir_log                           : "/var/log/oauth2-proxy/"
oauth2_config_path                       : "/var/oauth2_proxy/oauth2_config.cfg"
oauth2_compress_filename                 : "{{ oaut2_proxy_http | basename }}"
oauth2_filename                          : "{{ oauth2_compress_filename |replace('.tar.gz', '') }}"
oauth2_init_system                       : "systemd" # could be `systemd`, `sysv` or `no` for no setup

# See for all options https://raw.githubusercontent.com/bitly/oauth2_proxy/master/contrib/oauth2_proxy.cfg.example
oauth2_proxy_config                      :
    http_address                         : "127.0.0.1:5000"
    upstreams                            : [ "127.0.0.1:6060" ]
    provider                             : "github"
    email_domains                        : "*"
    cookie_secure                        : false
    cookie_domain                        : "localhost:5000"
    cookie_secret                        : "{{ 'COOK_SECRET' | b64encode }}"
    client_id                            : "YOUR_CLIENT_ID"
    client_secret                        : "CLIENT_SECERET"

oauth2_config_cmdline_args               : "-github-org='MYCoolORg'"
```

## Development

You can use the [Vagrantfile](Vagrantfile) for local testing, just install vagrant and virtualbox and execute the following commands.

````bash
vagrant up
vagrant provision
````

## License

MIT
