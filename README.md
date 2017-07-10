# ansible-role-resilio-sync

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-resilio-sync.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-resilio-sync)

RHEL/CentOS - All your data across all your devices

## Requirements

None

## Role Variables

Available variables are listed below, along with default values.

    rslsync_device_name: "{{ inventory_hostname }}"
    rslsync_directory_root: /
    rslsync_directory_root_policy: all
    rslsync_download_limit: 0
    rslsync_listening_port: 0
    rslsync_pid_file: /var/run/resilio-sync/sync.pid
    rslsync_shared_folders: []
    rslsync_storage_path: /var/lib/resilio-sync/
    rslsync_upload_limit: 0
    rslsync_use_upnp: True
    rslsync_advanced_options: {}
    rslsync_webui_bind_ip: 127.0.0.1
    rslsync_webui_port: 8888
    rslsync_webui_login: admin
    rslsync_webui_password: admin
    rslsync_webui_allow_empty_password: False

Advanced options is key/val list. You can use any valid options from [documentation](https://help.resilio.com/hc/en-us/articles/207371636-Power-user-preferences)

    rslsync_advanced_options:
        lan_encrypt_data: False
        disk_low_priority: True

## Dependencies

None

## Example Playbook

### With shared folders
    - hosts: servers
      roles:
        - role: linuxhq.resilio-sync
          rslsync_device_name: "{{ inventory_hostname.split('.')[0] }}"
          rslsync_listening_port: 6881
          rslsync_advanced_options:
            lan_encrypt_data: False
            disk_low_priority: True
          rslsync_shared_folders:
            - dir: /usr/local/etc/
              use_relay_server: False
              use_tracker: False
              search_lan: False
              use_sync_trash: False
              overwrite_changes: False
              selective_sync: False
              known_hosts:
                - name: rslsync1.linuxhq.org
                  port: 6881
                  secret: ADUGZGNAWRX4TLRR6523SVSGZLXJYGBCF
                - name: rslsync2.linuxhq.org
                  port: 6881
                  secret: B2O7EQSBFIGLM4K5SMZVB625MY7X3KUOI
                - name: rslsync3.linuxhq.org
                  port: 6881
                  secret: B2O7EQSBFIGLM4K5SMZVB625MY7X3KUOI
                  
### With Web UI
    - hosts: servers
      roles:
        - role: linuxhq.resilio-sync
          rslsync_device_name: "{{ inventory_hostname.split('.')[0] }}"
          rslsync_listening_port: 6881
          rslsync_webui_bind_ip: 0.0.0.0
          rslsync_webui_port: 8888
          rslsync_webui_login: admin
          rslsync_webui_password: admin
          rslsync_webui_allow_empty_password: false
          rslsync_advanced_options:
            lan_encrypt_data: False
            disk_low_priority: True

## License

BSD

## Author Information

This role was created by [Taylor Kimball](http://www.linuxhq.org).
