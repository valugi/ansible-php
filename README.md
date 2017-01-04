nobelbiocare.php
=========

Install php with optional php-fpm processor configuration using the IUS repository.

Requirements
------------

None

Role Variables
--------------
```yaml
install_php_fpm: no
install_xdebug: no

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

xdebug_package: php70u-xdebug

php_expose_php: "On"
php_max_execution_time: "30"
php_max_input_time: "60"
php_memory_limit: "128M"
php_error_reporting: "E_ALL & ~E_DEPRECATED & ~E_STRICT"
php_display_errors: "Off"
php_log_errors: "On"
php_log_errors_max_len: "1024"
php_ignore_repeated_errors: "Off"
php_ignore_repeated_source: "Off"
php_report_memleaks: "On"
php_track_errors: "Off"
php_html_errors: "On"
php_error_log: "syslog"
php_post_max_size: "8M"
php_include_path: "."
php_file_uploads: "On"
php_upload_max_filesize: "2M"
php_max_file_uploads: "20"
php_allow_url_fopen: "On"
php_allow_url_include: "Off"
php_default_socket_timeout: "60"
php_date_timezone: "UTC"
php_pdo_mysql_default_socket: ""
php_phar_readonly: "On"
php_sendmail_path: "/usr/sbin/sendmail -t -i"
php_mail_add_x_header: "On"
php_session_save_handler: "files"
php_session_save_path: "/tmp"
php_session_use_strict_mode: "0"
php_session_use_cookies: "1"
php_session_use_only_cookies: "1"
php_session_upload_progress_enabled: "On"
php_session_upload_progress_cleanup: "On"
php_session_upload_progress_prefix: "upload_progress_"
php_session_upload_progress_name: "PHP_SESSION_UPLOAD_PROGRESS"
php_session_upload_progress_freq: "1%"
php_session_upload_progress_min_freq: "1"
php_soap_wsdl_cache_enabled: "1"
php_soap_wsdl_cache_dir: "/tmp"
php_soap_wsdl_cache_ttl: "86400"
php_soap_wsdl_cache_limit: "5"

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

php_xdebug_version: 2.5.0
php_xdebug_module_path: /usr/lib64/php/modules
php_xdebug_config_filename: xdebug.ini
php_xdebug_coverage_enable: 1
php_xdebug_default_enable: 1
php_xdebug_cli_enable: 1
php_xdebug_remote_enable: 1
php_xdebug_remote_connect_back: 1
php_xdebug_remote_host: localhost
php_xdebug_remote_port: 9000
php_xdebug_remote_log: /var/log/xdebug.log
php_xdebug_remote_autostart: "false"
php_xdebug_scream: 1
php_xdebug_idekey: "PHPSTORM"
php_xdebug_max_nesting_level: 256
php_xdebug_show_local_vars: 0
```


Dependencies
------------

none

Example Playbook
----------------
```yaml
- hosts: php
  roles:
    - { name: nobelbiocare.php, install_php_fpm: yes, install_xdebug: yes }
```


License
-------

GPLv3

Author Information
------------------

Haydar Ciftci <haydar.ciftci@nobelbiocare.com>
