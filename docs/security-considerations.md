# Security Considerations

This lab is focused on secure remote access and should be treated as security‑sensitive from day one.

## Control Plane Protection

- Restrict access to the NetBird web UI to trusted source IP ranges or via an additional SSO / VPN layer.
- Enforce strong admin credentials and MFA where available.
- Regularly update the NetBird server OS and packages; monitor vendor advisories for security fixes.

## Overlay Network Design

- Separate client groups (e.g. admins, investigators, automation) into different access policies.
- Grant access on a "least privilege" basis, per subnet and per service, not "full LAN" by default.
- Use short‑lived access tokens and revoke devices immediately when lost or compromised.

## pfSense Edge Hardening

- Only allow overlay subnets that are strictly needed (avoid `0.0.0.0/0` style policies).
- Log all traffic between overlay and LAN and forward logs to a central SIEM for correlation.
- Combine this lab with existing IDS/IPS or DNS filtering (e.g. Suricata, Pi‑hole) where appropriate.

## Incident Response Readiness

- Time‑sync all components (OCI VM, pfSense, clients) using NTP to keep logs correlated.
- Periodically test access revocation (disable a client and confirm it cannot reach the LAN).
- Keep runbooks for how to temporarily shut down overlay access in case of suspected compromise.
