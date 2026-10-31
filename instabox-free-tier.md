# InstaBox free tier: limits and keepalive

Verified on a free machine (4 vCPU / 8 GiB / 20 GiB, Debian 13):
- Idle pause after 1800 s; continuous-run cap of 480 min, then a cooldown of ~10 min before it can start again. Plan for a short outage every 8 hours.
- The top level of `/data` is NOT writable by the guest user despite the docs — put persistent work under `/data/home`.
- No public inbound IPv4; reach services through the published HTTPS gateway URLs (the gateway terminates TLS and forwards WebSocket upgrades).
- Keepalive pattern: a scheduler execs the service's idempotent start script every 10 min. The exec itself counts as platform activity, wakes a paused machine, and self-heals a dead process. Stay silent on success; only report after two consecutive failures, and treat a single 409 `machine_cooldown` as routine.
- Idempotency pitfall: `pgrep -f` patterns must match the real command line. Starting via a relative path (`./xray run`) while checking for an absolute pattern never matches — every keepalive round spawned a duplicate. Start by absolute path and check for that same absolute pattern.
