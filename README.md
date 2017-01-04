nobelbiocare.php
=========

Install php with optional php-fpm processor configuration using the IUS repository.

Requirements
------------

None

Role Variables
--------------
```yaml
install_php_fpm: yes

php_packages:
  - php70u-bcmath
  - php70u-cli
  - php70u-common
  - php70u-gd
  - php70u-mbstring
  - php70u-mcrypt
  - php70u-mysqlnd
  - php70u-opcache
  - php70u-pdo
  - php70u-pear
  - php70u-process
  - php70u-soap
  - php70u-xml
  - php70u-xmlrpc
  - php70u-json

php_fpm_package: php70u-fpm

fpm_include: /etc/php-fpm.d/*.conf
fpm_pid: /run/php-fpm/php-fpm.pid
fpm_error_log: /var/log/php-fpm/error.log
fpm_syslog_facility: daemon
fpm_syslog_ident: php-fpm
fpm_log_level: notice
fpm_emergency_restart_threshold: 0
fpm_emergency_restart_interval: 0
fpm_process_control_timeout: 0
fpm_process_max: 128
fpm_process_priority: -19
fpm_daemonize: yes
fpm_rlimit_files: 1024
fpm_rlimit_core: 0
fpm_events_mechanism: epoll
fpm_systemd_interval: 10
  
php_fpm_pools: 
    - name: www
      access_format: "%R - %u %t \\%m %r\\ %s"
      access_log: /var/log/$pool.access.log
      catch_workers_output: "no"
      #chdir: /var/www
      #chroot: 
      #clear_env: "yes"
      group: php-fpm
      listen: 127.0.0.1:9000
      #listen_acl_groups: 
      #listen_acl_users: apache,nginx
      listen_allowed_clients: 127.0.0.1
      listen_backlog: 511
      listen_group: root
      listen_mode: 0660
      listen_owner: root
      #ping_path: 
      #ping_response: /ping
      pm: dynamic
      pm_max_children: 50
      pm_max_requests: 0
      pm_max_spare_servers: 35
      pm_min_spare_servers: 5
      #pm_process_idle_timeout: 10s
      pm_start_servers: 5
      #pm_status_path: /status
      #prefix: 
      #request_slowlog_timeout: 0
      #request_terminate_timeout: 0
      #rlimit_core: 
      #rlimit_files: 
      #security_limit_extensions: 
      slowlog: /var/log/www-slow.log
      user: php-fpm
      env: []

      php_admin_flag: 
        - log_errors: "on"

      php_admin_value:
        - error_log: /var/log/www-error.log
          #memory_limit: 128M

      php_flag: []

      php_value: 
        - session.save_handler: files
        - session.save_path: /var/lib/php/fpm/session
        - soap.wsdl_cache_dir: /var/lib/php/fpm/wsdlcache
```


Dependencies
------------

none

Example Playbook
----------------
```yaml
- hosts: php
  roles:
    - { name: nobelbiocare.php, install_php_fpm: yes }
```


License
-------

GPLv3

Author Information
------------------

Haydar Ciftci <haydar.ciftci@nobelbiocare.com>
