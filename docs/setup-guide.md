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

sudo apt update && sudo apt upgrade -y

## 3. Install NetBird Management Server

1. Follow the official NetBird installation script for Debian/Ubuntu.
2. During installation, set the public URL to your Cloudflare DNS name, e.g. `https://netbird.example.com`.
3. Verify that the NetBird web UI is reachable over HTTPS from the internet.

> In the original lab this step was first done on a home Linux box behind pfSense;  
> moving it to OCI eliminated issues with power cuts and unstable upstream bandwidth.

## 4. Integrate with Cloudflare DNS

1. Create an `A` record in Cloudflare:
   - Name: `netbird`
   - Content: public IP of the OCI VM
2. Optionally enable Cloudflare proxy if compatible with your NetBird configuration.
3. Confirm that `netbird.example.com` resolves correctly and reaches the VM.

## 5. Register pfSense as a Routing Peer

1. Install the NetBird agent on a small Linux VM behind pfSense, or directly on pfSense if supported.
2. Join this node to the NetBird network using the web UI or enrollment key.
3. In the NetBird admin UI, mark this node as a **route provider** for the internal LAN subnet, e.g. `10.20.0.0/24`.
4. On pfSense, add static routes / firewall rules as needed to allow traffic between:
   - NetBird overlay subnet (e.g. `100.64.0.0/10`)
   - Internal LAN (`10.20.0.0/24`)

## 6. Connect Remote Clients

1. Install NetBird clients on laptops / workstations.
2. Enroll each client using the NetBird web UI.
3. Assign access policies so that only authorised clients can reach the routed LAN subnet.

Test by:

- Pinging internal hosts (e.g. `10.20.0.10`) from a client.
- Accessing web services or admin interfaces that previously were only reachable on‑site.
