# Pitfalls & Migration Notes

The first version of this lab used a home Linux box as the NetBird management server, sitting behind pfSense and CGNAT.  
While it worked for short tests, several issues appeared in practice:

## 1. Home‑Hosted Control Plane Issues

- Power outages and router reboots regularly broke the control plane.
- Consumer ISP uplink was too unstable for long‑lived sessions.
- Dynamic IP changes required manual DNS updates.

## 2. Benefits of Moving to OCI

- Stable power and public IP for the NetBird server.
- Clear separation between **control plane** (OCI) and **edge nodes** (pfSense, clients).
- Easier to integrate with Cloudflare and automate TLS certificates.

## 3. Design Recommendations

- Always place the NetBird / ZTNA control plane on reliable infrastructure (cloud or datacentre).
- Treat pfSense and home servers as edge routers only.
- Keep good logging on both NetBird and pfSense to support incident response and audits.
