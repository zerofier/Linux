# Linux

## semanage boolean
    semanage boolean -l | grep httpd
    httpd_can_network_relay        (off  ,  off)  Allow httpd to can network relay
    httpd_can_connect_mythtv       (off  ,  off)  Allow httpd to can connect mythtv
    httpd_can_network_connect_db   (off  ,  off)  Allow httpd to can network connect db
    httpd_use_gpg                  (off  ,  off)  Allow httpd to use gpg
    httpd_dbus_sssd                (off  ,  off)  Allow httpd to dbus sssd
    httpd_enable_cgi               (on   ,   on)  Allow httpd to enable cgi
    httpd_verify_dns               (off  ,  off)  Allow httpd to verify dns
    httpd_dontaudit_search_dirs    (off  ,  off)  Allow httpd to dontaudit search dirs
    httpd_use_cifs                 (off  ,  off)  Allow httpd to use cifs
    httpd_manage_ipa               (off  ,  off)  Allow httpd to manage ipa
    httpd_run_stickshift           (off  ,  off)  Allow httpd to run stickshift
    httpd_enable_homedirs          (off  ,  off)  Allow httpd to enable homedirs
    httpd_dbus_avahi               (off  ,  off)  Allow httpd to dbus avahi
    httpd_unified                  (on   ,   on)  Allow httpd to unified
    httpd_mod_auth_pam             (on   ,   on)  Allow httpd to mod auth pam
    httpd_can_network_connect      (on   ,  off)  Allow httpd to can network connect
    httpd_execmem                  (off  ,  off)  Allow httpd to execmem
    httpd_use_fusefs               (off  ,  off)  Allow httpd to use fusefs
    httpd_mod_auth_ntlm_winbind    (off  ,  off)  Allow httpd to mod auth ntlm winbind
    httpd_use_sasl                 (off  ,  off)  Allow httpd to use sasl
    httpd_tty_comm                 (off  ,  off)  Allow httpd to tty comm
    httpd_sys_script_anon_write    (off  ,  off)  Allow httpd to sys script anon write
    httpd_graceful_shutdown        (on   ,   on)  Allow httpd to graceful shutdown
    httpd_can_connect_ftp          (off  ,  off)  Allow httpd to can connect ftp    
    httpd_run_ipa                  (off  ,  off)  Allow httpd to run ipa
    httpd_read_user_content        (off  ,  off)  Allow httpd to read user content
    httpd_use_nfs                  (off  ,  off)  Allow httpd to use nfs
    httpd_can_connect_zabbix       (off  ,  off)  Allow httpd to can connect zabbix
    httpd_tmp_exec                 (off  ,  off)  Allow httpd to tmp exec
    httpd_run_preupgrade           (off  ,  off)  Allow httpd to run preupgrade
    httpd_can_sendmail             (off  ,  off)  Allow httpd to can sendmail
    httpd_builtin_scripting        (on   ,   on)  Allow httpd to builtin scripting
    httpd_can_connect_ldap         (off  ,  off)  Allow httpd to can connect ldap
    httpd_can_check_spam           (off  ,  off)  Allow httpd to can check spam
    httpd_can_network_memcache     (off  ,  off)  Allow httpd to can network memcache
    httpd_can_network_connect_cobbler (off  ,  off)  Allow httpd to can network connect cobbler
    httpd_anon_write               (off  ,  off)  Allow httpd to anon write
    httpd_serve_cobbler_files      (off  ,  off)  Allow httpd to serve cobbler files
    httpd_ssi_exec                 (off  ,  off)  Allow httpd to ssi exec
    httpd_use_openstack            (off  ,  off)  Allow httpd to use openstack
    httpd_enable_ftp_server        (off  ,  off)  Allow httpd to enable ftp server
    httpd_setrlimit                (off  ,  off)  Allow httpd to setrlimit


## selinux module

    module httpd 1.0;
    
    require {
            type user_cron_spool_t;
            type initrc_tmp_t;
            type mysqld_port_t;
            type httpd_t;
            type httpd_sys_content_t;
            type initrc_t;
            type shadow_t;
            class sock_file write;
            class unix_stream_socket connectto;
            class dir { add_name create remove_name write };
            class file { append create open read rename setattr unlink write };
            class tcp_socket name_connect;
    }
    
    #============= httpd_t ==============
    
    #!!!! This avc is allowed in the current policy
    allow httpd_t httpd_sys_content_t:dir { add_name create remove_name write };
    
    #!!!! This avc is allowed in the current policy
    allow httpd_t httpd_sys_content_t:file { append create rename setattr write };
    
    #!!!! This avc is allowed in the current policy
    allow httpd_t initrc_t:unix_stream_socket connectto;
    
    #!!!! This avc is allowed in the current policy
    allow httpd_t initrc_tmp_t:sock_file write;
    
    #!!!! This avc is allowed in the current policy
    allow httpd_t mysqld_port_t:tcp_socket name_connect;
    
    #!!!! This avc is allowed in the current policy
    allow httpd_t shadow_t:file { open read };
    
    #!!!! This avc is allowed in the current policy
    allow httpd_t user_cron_spool_t:dir { add_name remove_name write };
    allow httpd_t user_cron_spool_t:file { rename unlink };
    
    #!!!! This avc is allowed in the current policy
    allow httpd_t user_cron_spool_t:file { create open setattr };
