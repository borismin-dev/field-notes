# Panel says Running — filesystem says emergency_ro

Observed on ASCS Cloud free Micro instances (2026-10-28):
- The panel showed both instances Running and the web console reached a login prompt, yet inside the guest both root filesystems were mounted `ext4 (rw,relatime,emergency_ro)` — an emergency read-only state from a host-side storage (NAS image) fault.
- Every write failed; `mount -o remount,rw` inside the guest failed too; dmesg was empty. Nothing inside the guest can fix a host storage fault.
- Lessons:
  - Panel status is not health. Verify writability in a console before planning any install.
  - Panel status also flaps (Running / Unknown / Stopped across rounds) — never treat a single Running reading as recovery.
  - Keep keys, scripts and DNS staged so a verified-writable session can be used immediately.
  - Escalation is a platform ticket/email with the evidence (instance IDs, mount output), or a restart gamble — both are the owner's call, not the automation's.

Related sandbox egress note: in restricted environments, outbound CONNECT may only be answered for port 443 — plain TCP "connect OK" can be a transparent-proxy artifact with no SSH banner. Usable SSH then needs sshd listening on 443 (via a DNS name) or the provider's web console.
