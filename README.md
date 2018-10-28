# ansible-freebsd-acme-client

## Introduction
This role installs `acme-client` on FreeBSD and configure a list of certificates to be generated and kept up to date using [periodic](https://www.freebsd.org/cgi/man.cgi?periodic%288%29).

It's by default meant to be used with nginx, but any web server works as well, provided you do the configuration yourself.

## Variables

See [defaults/main.yml](defaults/main.yml) for the default values of each.

### acme_client_domains

This variable is used to list the domains you want to get certificates for.

### acme_client_use_internal_http_server

If true, the role will use python as an HTTP server when creating the key and certificate the first time.

Set it to false if you already have a HTTP server serving path `/.well-known/acme-challenge/` on port 80 for your domains.

### acme_client_deploy_script

Contains the script that is executed after the renew script is called.

## Example

    acme_client_domains:
      - domain: example.com
        aliases: ns1.example.com ns2.example.com ftp.example.com www.example.com
      - domain: example.net
        aliases: jambon.example.net truite.example.net poulet.example.net
    acme_client_use_internal_http_server: yes
    acme_client_deploy_script: |
		#!/bin/sh
	     
		set -e
	     
		/usr/sbin/service my_service_using_the_certs reload

## Dependencies

None.

## Licence

BSD

## Author

[Erwan Martin](https://zewaren.net/)
