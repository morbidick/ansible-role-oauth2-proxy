# bitly OAuth2-proxy ansible role

[![Build Status](https://travis-ci.org/morbidick/ansible-role-oauth2-proxy.svg?branch=master)](https://travis-ci.org/morbidick/ansible-role-oauth2-proxy)

An ansible role to install and configure [oauth2 proxy](https://github.com/pusher/oauth2_proxy).

## Variables

```yaml
oauth2_user                              : "oauth2"
oauth2_dir                               : "/opt/oauth2_proxy"
oauth2_tmp_dir                           : "/opt/oauth2_proxy/tmp"
oauth2_log_dir                           : "/var/log/oauth2-proxy/"
oauth2_config_path                       : "/etc/oauth2_proxy/oauth2_config.cfg"
oauth2_init_system                       : "systemd" # could be `systemd`, `sysv` or `no` for no setup

# See for all options https://raw.githubusercontent.com/pusher/oauth2_proxy/master/contrib/oauth2_proxy.cfg.example
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

To test the oauth2 procedure against Github create a new OAuth application in your [profile](https://github.com/settings/developers) with the homepage `http://127.0.0.1:5000` and callback url `http://127.0.0.1:5000/oauth2/callback`. Replace `client_id` and `client_secret` in [tests/role.yml](tests/role.yml) with the provided github tokens. Open your browser at [127.0.0.1:5000](http://127.0.0.1:5000)

## License

MIT
