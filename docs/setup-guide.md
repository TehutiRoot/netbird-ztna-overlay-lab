# Setup Guide – NetBird ZTNA Overlay with pfSense & OCI

## 1. Environment Overview

- **Cloud control plane**
  - OCI free‑tier VM (Debian/Ubuntu)
  - Public DNS name via Cloudflare (e.g. `netbird.example.com`)
- **Edge / on‑prem**
  - pfSense firewall behind CGNAT
  - Home / SME LAN subnet (e.g. `10.20.0.0/24`)
- **Clients**
  - NetBird clients on laptops / investigation workstations

All IPs and names in this document are examples only.

## 2. Provision Debian VM on OCI

1. Create a small VM (1 OCPU, 1 GB RAM) in OCI.
2. Assign a public IP and open inbound ports for:
   - TCP 80/443 (initial setup / HTTPS)
   - UDP 443 or 51820 (NetBird wire protocol, depending on configuration)
3. Update the system:

