# Ansible Role: HAProxy Load Balancer

Ansible role for deploying and configuring HAProxy load balancer with TLS termination, Certbot SSL hooks, Prometheus exporter for Grafana monitoring, and Keepalived VRRP high-availability clustering.

## Features

- **TLS Termination**: Serves SSL/TLS certificates (e.g. Certbot / Let's Encrypt) on port `8006` with WebSocket support for Proxmox NoVNC/SPICE consoles.
- **Certbot Renewal Hook**: Automatically concatenates updated `fullchain.pem` and `privkey.pem` into HAProxy PEM format upon renewal and reloads HAProxy.
- **Prometheus Metrics**: Built-in Prometheus exporter service on port `8404` at endpoint `/metrics`.
- **Keepalived VRRP**: Configures Keepalived virtual IP failover across HAProxy cluster nodes.

## Role Variables

See `defaults/main.yml` for the complete list of configurable variables:

```yaml
haproxy_frontend_domain: "proxmox.pve.infra.clawduino.com"
haproxy_frontend_port: 8006
haproxy_ssl_cert_path: "/etc/haproxy/certs/proxmox.pve.infra.clawduino.pem"
haproxy_prometheus_exporter_enabled: true
haproxy_prometheus_port: 8404
haproxy_keepalived_enabled: true
haproxy_keepalived_vip: "10.1.0.137/23"
```

## Example Playbook

```yaml
- hosts: haproxy_nodes
  become: true
  roles:
    - role: ansible-role-haproxy
```
