# NetBird ZTNA Overlay Lab – pfSense, OCI & Cloudflare

## Overview

This lab shows how to build a zero‑trust overlay network using a self‑hosted NetBird management server in the cloud, pfSense as an on‑premise router, and Cloudflare‑managed DNS.  
It started as a home‑server experiment and was later migrated to an OCI VM to avoid power/ISP instability at home and to provide a more production‑ready control plane.

## Goals

- Provide secure remote access to a home/SME network that sits behind CGNAT, without opening any public ports on pfSense.  
- Demonstrate how to move from a fragile home‑hosted NetBird setup to a stable, cloud‑hosted management plane.  
- Serve as a reusable blueprint for incident response teams, law‑enforcement units and high‑trust freelance work.

## High‑Level Architecture

- **NetBird Management Server** running on a Debian/Ubuntu VM in OCI.  
- **pfSense** acting as a routing peer into the internal LAN/DMZ.  
- **Cloudflare / public DNS** providing a friendly hostname and TLS for the NetBird web UI and control endpoints.  
- **Remote clients** (laptops, investigation workstations, admin machines) joining the overlay and reaching internal services via routed subnets.

## Why move from home server to cloud?

Initial tests used a home‑hosted Linux box as the NetBird server, behind pfSense and CGNAT.  
While functional, it suffered from power cuts, consumer‑grade ISP issues and limited upstream bandwidth.  
Migrating the management plane to OCI solved these problems and turned the home network into just another secure edge node.

## Related Projects in this Series

## Related Projects in this Series

- **Digital Raid Lab – WireGuard & pfSense**  
  WireGuard + pfSense + OCI lab for exposing services behind CGNAT using encrypted tunnels and port-forwarding with full network-forensics workflows.  
  Repo: https://github.com/TehutiRoot/digital-raid-lab-wireguard-pfsense




## Repository Layout (planned)

- `docs/` – Setup guides for Debian VM, NetBird installation, pfSense routing peer, and Cloudflare integration.  
- `configs/` – Sanitised example configs (NetBird routes, pfSense static routes, firewall rules).  
- `pitfalls/` – Notes on what did not work well on the home‑server design and how the cloud‑hosted version fixes it.

This lab complements the **digital‑raid‑lab‑wireguard‑pfsense** repository by focusing on identity‑aware access (ZTNA) instead of pure tunnel and port‑forwarding.
