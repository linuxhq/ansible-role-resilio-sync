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

## Dependencies

None

## Example Playbook

    - hosts: servers
      roles:
        - role: linuxhq.resilio-sync
          rslsync_device_name: "{{ inventory_hostname.split('.')[0] }}"
          rslsync_listening_port: 6881
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

## License

BSD

## Author Information

This role was created by [Taylor Kimball](http://www.linuxhq.org).
