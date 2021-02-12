# ansible-role-resilio_sync

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-resilio_sync.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-resilio_sync)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-resilio_sync-blue.svg?style=flat)](https://galaxy.ansible.com/linuxhq/resilio_sync)
[![License](https://img.shields.io/badge/license-GPLv3-brightgreen.svg?style=flat)](COPYING)

RHEL/CentOS - All your data across all your devices

## Requirements

None

## Role Variables

Available variables are listed below, along with default values.

    rslsync_bind_interface: "{{ ansible_default_ipv4.interface }}"
    rslsync_config_refresh_interval: 3600
    rslsync_config_save_interval: 600
    rslsync_device_name: "{{ inventory_hostname }}"
    rslsync_direct_torrent_enabled: true
    rslsync_directory_root: /
    rslsync_directory_root_policy: all
    rslsync_disable_remove_from_all_devices: false
    rslsync_disk_low_priority: false
    rslsync_disk_min_free_space: '0'
    rslsync_disk_min_free_space_gb: 0
    rslsync_download_limit: 0
    rslsync_enable_file_system_notifications: true
    rslsync_enable_warning_no_source: true
    rslsync_external_port: 0
    rslsync_fix_conflicting_paths: true
    rslsync_folder_defaults_delete_unknown_files: false
    rslsync_folder_defaults_known_hosts: []
    rslsync_folder_defaults_use_relay: true
    rslsync_folder_defaults_use_tracker: true
    rslsync_folder_rescan_interval: 600
    rslsync_free_space_warning_threshold: 1024
    rslsync_groups: []
    rslsync_ignore_symlinks: false
    rslsync_keep_expired_transfer_days: 0
    rslsync_lan_encrypt_data: true
    rslsync_lazy_indexing: true
    rslsync_log_size: 100
    rslsync_log_ttl: 7
    rslsync_listening_port: 0
    rslsync_max_file_size_for_versioning: 1000
    rslsync_max_packet_size: 32
    rslsync_max_torrent_metadata_size: 16
    rslsync_net_udp_ipv4_mtu: 1500
    rslsync_net_udp_ipv6_mtu: 1500
    rslsync_normalize_unicode_paths: true
    rslsync_overwrite_changes: false
    rslsync_parallel_indexing: false
    rslsync_peer_expiration_days: 7
    rslsync_pid_file: /var/run/resilio-sync/sync.pid
    rslsync_prefer_utp2_lan: false
    rslsync_prioritize_initial_indexing: false
    rslsync_profiler_enabled: false
    rslsync_proxy: {}
    rslsync_rate_limit_local_peers: false
    rslsync_send_statistics: true
    rslsync_share_file_ttl: 3
    rslsync_shared_folders: {}
    rslsync_show_service_disk_thread: false
    rslsync_storage_path: /var/lib/resilio-sync/
    rslsync_sync_extended_attributes: true
    rslsync_sync_max_time_diff: 600
    rslsync_sync_trash_ttl: 30
    rslsync_torrent_max_piece_size: 2097152
    rslsync_torrent_piece_size_policy: 0
    rslsync_transfer_job_skip_locked_files: false
    rslsync_tunnel_compress_delay_size: 102400
    rslsync_tunnel_compress_delay_time: 10000
    rslsync_tunnel_compress_stream: false
    rslsync_upload_limit: 0
    rslsync_use_only_bind_interface: false
    rslsync_use_upnp: true
    rslsync_webui:
      allow_empty_password: false
      listen: '0.0.0.0:8888'
      login: admin
      password: admin
    rslsync_worker_threads_count: 0

## Dependencies

None

## Example Playbook

### With shared folders

    - hosts: servers
      roles:
        - role: linuxhq.resilio_sync
          rslsync_device_name: "{{ inventory_hostname.split('.')[0] }}"
          rslsync_groups:
            - couchpotato
            - medusa
          rslsync_listening_port: 6881
          rslsync_shared_folders:
            data:
              dir: /mnt/data
              known_hosts: "{{ groups['media'] }}"
              overwrite_changes: false
              search_lan: false
              secret: ADUGZGNAWRX4TLRR6523SVSGZLXJYGBCF
              selective_sync: false
              use_relay_server: false
              use_sync_trash: false
              use_tracker: false
          rslsync_webui: {}

### With Web UI

    - hosts: servers
      roles:
        - role: linuxhq.resilio_sync
          rslsync_device_name: "{{ inventory_hostname.split('.')[0] }}"
          rslsync_groups:
            - couchpotato
            - medusa
          rslsync_listening_port: 6881
          rslsync_shared_folders: {}
          rslsync_webui:
            allow_empty_password: false
            listen: '0.0.0.0:8888'
            login: admin
            password: admin

## License

Copyright (C) 2018 Taylor Kimball <tkimball@linuxhq.org>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program. If not, see <http://www.gnu.org/licenses/>.
