# Home vs Cloud-Hosted Control Plane

## Home-Hosted NetBird (Initial Attempt)

Pros:
- Easy to start with existing hardware.
- No additional cloud cost for small tests.

Cons observed in this lab:
- Depended on consumer power and ISP quality.
- Required manual workarounds for dynamic IP and port-forwarding.
- Harder to maintain acceptable uptime for serious investigations or business use.

## Cloud-Hosted NetBird on OCI

Pros:
- Stable public endpoint with predictable uptime.
- Clean separation of responsibilities: cloud = control plane, pfSense = edge router.
- Easier integration with Cloudflare DNS and certificate automation.

Cons:
- Additional surface area to secure (public VM on the internet).
- Requires ongoing patching and monitoring of the cloud VM.

## Recommendation

Use home‑hosted control planes only for learning and small PoCs.  
For anything that involves real incidents, paying clients, or law‑enforcement work, move the management plane to a hardened, monitored cloud VM and treat pfSense/home systems strictly as edge nodes.
