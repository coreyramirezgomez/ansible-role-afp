AFP
=========

Install and configure AFP server with netatalk pacakge.

## Requirements

- Full privileges to install packages on target host.
- Full privileges to write to protected files under /etc/

## Role Variables

All defaults can be found here: http://netatalk.sourceforge.net/3.0/htmldocs/afp.conf.5.html
```
afp_admin_group: ""
afp_save_password: "yes"
afp_log_file: "/var/log/afpd.log"
afp_log_level: "default"
afp_log_level_type: "severe"
afp_fqdn: ""
afp_uam_guest: no
afp_uam_clear_text: no
afp_uam_randum: no
afp_uam_dhx: yes
afp_uam_dhx2: yes
afp_uam_k5: no
afp_uam_path: ""
afp_kerberos:
  k5_keytab: "/etc/krb5/krb5.keytab"
  k5_service: "afpserver"
  k5_realm: ""
afp_spotlight: "yes"
```
### LDAP
See for details: http://netatalk.sourceforge.net/3.0/htmldocs/afp_ldap.conf.5.html
```
afp_ldap:
  ldap_auth_method: "simple"
  ldap_auth_dn: ""
  ldap_auth_pw: ""
  ldap_server: ""
  ldap_userbase: []
  ldap_userscope: ""
  ldap_user_filter: ""
  ldap_name_attr: "uid"
  ldap_groupbase: []
  ldap_group_scope: ""
  ldap_group_filter: ""
  ldap_group_attr: "cn"
  ldap_uuid_attr: "ObjectGUID"
  ldap_uuid_encoding: ""
  map_acls: "mode"
```
### Mounts
List of dictionaries for every mount to configure.
```
afp_mounts:
  - title: ""
    path: ""
    dir_perm: ""
    file_perm: ""
    time_machine: no
    valid_users: []
    rw_list: []
    cnid_scheme: "dbd"
    basedir_regex: ""
    vol_size_limit: ""
```

Coming soon...for now see defaults/main.yml

## Example Playbook

    - hosts: afp_hosts
      roles:
        - role: coreyramirezgomez.afp
          afp_mounts:
            - title: "AFP Share"
              path: "/mnt/afp_share"
              dir_perm: "774"
              file_perm: "774"
              time_machine: no
              valid_users:
                - "@games"
              rw_list:
                - "@admins"
            - title: "Homes"
              basedir_regex: "/home"
              time_machine: no
            - title: "Delorean"
              path: "/mnt/delorean"
              dir_perm: "776"
              file_perm: "776"
              time_machine: yes
              valid_users:
                - "@timemachine"
              rw_list:
                - "@timemachine"
          ...
