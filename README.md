promtail_exporter
=========

Deploy Promtail agent onPrem installation (no container)

Requirements
------------

- Ansible 2.7 >=

Role Variables
--------------

All roles variables was described in default var file :

Required :

- **loki_server_url :** (url of your loki server http://loki:3100)
- **promtail_scrape_configs :** (specify scrape_configs for your promtail agent)

Optional :

- **loki_user :**   (Optional Default : loki)
- **loki_group :**  (Optional Default : loki)
- **promtail_base_dir :** (Optional Default : /opt/promtail)
- **promtail_config_dir :** (Optional Default : /etc/promtail)
- **promtail_log_dir :** (Optional Default : /var/log/promtail)
- **promtail_version :** (Optional Default : 1.4.1)
- **promtail_additional_groups :** (Optional Default : adm)
- **promtail_dist_url :** (Optional Default : "https://github.com/grafana/loki/releases/download/v<promtail_version>/promtail-linux-amd64.zip")


Dependencies
------------

NA

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
    - hosts: frontend
      vars:
        promtail_force_directory_rights:
          - /var/myapp/platform/log
        promtail_scrape_configs: |
        - job_name: system
          entry_parser: raw
          static_configs:
          - targets:
              - frontend
            labels:
              job: varlogs
              host: "{{ inventory_hostname }}"
              __path__: /var/log/*log
        - job_name: ohp
          entry_parser: raw
          static_configs:
          - targets:
              - frontend
            labels:
              job: ohp_logs
              host: "{{ inventory_hostname }}"
              __path__: /var/myapp/platform/log/*.log
      roles:
      - role: promtail-exporter
```



License
-------

BSD

Author Information
------------------

ohhfrancois

Molecule Test
------------------

```bash
pip3 install molecule ansible ansible-lint docker
```