nginx
=========

Role to set up a nginx container with support for self-signed ssl certificates and let's encrypt wildcard certificate with dns challenge.

Limitations
-----------

The DNS challenge currently only supported netcup DNS with only one domain, which is configured with nginx_config_netcup_domain.

Requirements
------------

Docker and all dependencies to manage docker containers need to be installed on the target machine for this role to be working.

Role Variables
--------------

| Config Key                                      | Description                                                                        | Values | Default                                        |
|-------------------------------------------------|------------------------------------------------------------------------------------|--------|------------------------------------------------|
| nginx_container_name                            | The container name for the started nginx container.                                |        | nginx                                          |
| nginx_container_networks                        | The list of docker networks for the started container.                             |        |                                                |
| nginx_image_name                                | Override for the nginx image name. Use this if you want to provide your own image. |        | nginx                                          |
| nginx_image_tag                                 | The tag for the used nginx image.                                                  |        | stable                                         |
| nginx_config_expose_ports                       | List of exposed port in the docker format. (e.g. - "80:80")                        |        | - "80:80"<br/>- "443:443"                      |
| nginx_filesystem_root                           | The path on the filesystem for the nginx files.                                    |        |                                                |
| nginx_filesystem_sites                          | The path on the filesystem where the sites configurations are stored.              |        |                                                |
| nginx_filesystem_ssl                            | The path on the filesystem where SSL certificates are stored.                      |        |                                                |
| nginx_config_cert_email                         | The SSL certificate email.                                                         |        |                                                |
| nginx_config_letsencrypt_dns_challenge_provider | The provider for the letsencrypt dns challenge. Only netcup is current supported.  | netcup |                                                |
| nginx_config_letsencrypt_account_email          | The account email for lets encrypt.                                                |        |                                                |
| nginx_config_letsencrypt_acme_directory         | The letsencrypt acme directory. Can be staging or production.                      |        | https://acme-v02.api.letsencrypt.org/directory |
| nginx_config_sites                              | List of nginx sites                                                                |        |                                                |
| nginx_config_netcup_api_key                     | Netcup API key                                                                     |        |                                                |
| nginx_config_netcup_api_password                | Netcup API password                                                                |        |                                                |
| nginx_config_netcup_customer_id                 | Netcup customer id                                                                 |        |                                                |
| nginx_config_netcup_domain                      | Netcup domain                                                                      |        |                                                |

Variables for nginx_config_sites
--------------------------------

| Variable       | Description                                           | Values                   | Default |
|----------------|-------------------------------------------------------|--------------------------|---------|
| hostname       | The hostname for the site. Will also be the filename. |                          |         |
| ssl_provider   | Specify the ssl provider.                             | self-signed, letsencrypt |         |
| path_config    | List of path configs.                                 |                          |         |

Variables for path_config
-------------------------

| Variable      | Description                                                                                                   |
|---------------|---------------------------------------------------------------------------------------------------------------|
| location      | The http site location to be configured.                                                                      |
| proxy_pass    | The path for proxy_pass.                                                                                      |
| configuration | Additional nginx configuration for the path. They will be placed 1 to 1 into the path configuration in nginx. |

Example for nginx_config_sites
------------------------------

```yaml
nginx_config_sites:
  - hostname: my.domain.com
    ssl_provider: letsencrypt
    path_config:
      - location: "/"
        proxy_pass: "http://interal-host:8080"
      - location: "/my-grafana-installation"
        proxy_pass: "http://internal-host-2:3000"
        configuration:
          - "rewrite /grafana/(.*) /$1  break;"
```

Dependencies
------------

License
-------

MIT
