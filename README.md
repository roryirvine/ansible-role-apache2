# Ansible-Role-Apache

[![Build Status](https://travis-ci.org/comicrelief/ansible-role-apache2.svg?branch=master)](https://travis-ci.org/davidedimauro88/ansible-role-apache)

An Ansible Role that installs Apache 2.x on Debian/Ubuntu systems.

## Requirements
none
## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

**packages:**       - List of packages to install, including php5 package and modules. Default packages listed below:

    - apache2
    - curl
    - mysql-client
**http_port: 80**   - The port on which apache should be listening. (Required)

**dissite_apache:** - Dissite the default Apache's configuration. It won't if set as false. Default are:
      - 000-default
      - default-ssl

**apache_vhost:**
 
 *Additional optional properties*: 'aliases', 'auth', 'login_auth', 'newrelic', 'rewrite', 'folder', 'cdn'.
Set of properties per virtualhost: 'server_name' (required), 'document_root' (required).

Here's an example of what it should look like:

      - server_name: test
        document_root: /var/www/test/
        folder: public
        auth:
          htaccess:
            review: hav3al00k
          ip:
            forwarded:
              - name: CRAccess
                ip: 62.6.159.62
              - name: Test
                ip: 127.0.0.1
            direct: '127.0.0.1 127.0.1.1'
        newrelic: true
        elb: true
          - servername: "local.dev"
            documentroot: "/var/www/html"

Set a list of modules which need to be enabled for this Apache configuration:
    
    modules:
      - rewrite
      - remoteip
      - headers
      - expires
      - deflate

Add all the Apache modules you want to your vars file to enable them.

## Dependencies

None.

## Example Playbook

    - hosts: webservers
      vars_files:
        - vars/main.yml
      roles:
        - { role: ansible-role-apache }

*Inside `vars/main.yml`*:

    http_port: 8080
    apache_vhost:
      - {server_name: "example.com", document_root: "/var/www/vhosts/example_com"}

## License

MIT / BSD
