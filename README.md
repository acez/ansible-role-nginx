nginx
=========

Role to set up a nginx container with support for self-signed ssl certificates and let's encrypt wildcard certificate with netcup dns challenge.
This is very simple role to set up a nginx proxy with ssl for other docker services.

Requirements
------------

Docker and all dependencies to manage docker containers need to be installed on the target machine for this role to be working.

Role Variables
--------------

| Config Key                         | Description                                                                        | Default                   |
|------------------------------------|------------------------------------------------------------------------------------|---------------------------|
| nginx_container_name               | The container name for the started nginx container.                                | nginx                     |
| nginx_image_name                   | Override for the nginx image name. Use this if you want to provide your own image. | nginx                     |
| nginx_image_tag                    | The tag for the used nginx image.                                                  | stable                    |
| nginx_config_certbot_enabled       | If certbot is enabled, it will use dns challenge with the netcup dns api.          | false                     |
| nginx_config_expose_ports          | List of exposed port in the docker format. (e.g. - "80:80")                        | - "80:80"<br/>- "443:443" |
| nginx_config_cert_name             | The filename for the certificate.                                                  | default                   |
| nginx_filesystem_root              | The path on the filesystem for the nginx files.                                    |                           |
| nginx_filesystem_sites             | The path on the filesystem where the sites configurations are stored.              |                           |
| nginx_filesystem_ssl               | The path on the filesystem where SSL certificates are stored.                      |                           |
| nginx_filesystem_certbot           | The path on the filesystem where certbot files are stored.                         |                           |
| nginx_container_networks           | The list of docker networks for the started container.                             |                           |
| nginx_config_cert_common_name      | The SSL certificate common name.                                                   |                           |
| nginx_config_cert_email            | The SSL certificate email.                                                         |                           |
| nginx_config_certbot_account_email | The account email for lets encrypt.                                                |                           |
| nginx_config_netcup_api_key        | Netcup API key                                                                     |                           |
| nginx_config_netcup_api_password   | Netcup API password                                                                |                           |
| nginx_config_netcup_customer_id    | Netcup customer id                                                                 |                           |
| nginx_config_netcup_domain         | Netcup domain                                                                      |                           |

Dependencies
------------

License
-------

MIT
