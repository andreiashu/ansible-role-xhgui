# Ansible Role: xhgui

Installs xhgui.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    xhgui_composer_path: /usr/local/bin/composer

The path where composer will be installed and available to your system. It is where the xhgui library will be downloaded. Note that you will have to point your vhost to: `{{ xhgui_composer_path }}/vendor/perftools/xhgui/webroot`.

## Dependencies

Ansible roles:
 * [geerlingguy.php](https://github.com/geerlingguy/ansible-role-php)
 * [geerlingguy.composer](https://github.com/geerlingguy/ansible-role-composer)
 * [lesmyrmidons.mongodb](https://github.com/lesmyrmidons/ansible-role-mongodb)

## Example Playbook

    - hosts: servers
      vars_files:
        - vars/main.yml
      roles:
        - { role: geerlingguy.apache }
        - { role: andreiashu.xhprof }

*Inside `vars/main.yml`*:

    apache_listen_port: 80
    apache_vhosts:
    # setup the xhgui vhost
      - {servername: "xhgui.localdev.com", documentroot: "/usr/local/composer/vendor/perftools/xhgui/webroot"}

    # example of vhost that enables xhprof profiling
      - {
          servername: "myapp.localdev.com",
          documentroot: "/var/www/myapp/docroot",
          extra_parameters: "php_admin_value auto_prepend_file \"/usr/local/composer/vendor/perftools/xhgui/external/header.php\""
        }


## License

MIT / BSD

## Credits

Thanks to [@akrabat](https://twitter.com/akrabat), [Jeff Geerling](http://jeffgeerling.com/) and [Kevin ARBOUIN](https://github.com/lesmyrmidons) for their work in this space which helped me create this role.

## Author Information

This role was created by [Andrei Simion](https://twitter.com/andreiashu).
