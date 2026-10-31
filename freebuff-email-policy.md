# Freebuff sign-in and email policy (verified 2026-10-31)

- Freebuff has no email+password registration. Sign-in is only "Continue with GitHub" or Google.
- New accounts are rejected if the account's email is a temporary, disposable, privacy or alias provider — the error page names Proton Mail, Tutanota, DuckDuckGo and Firefox Relay (`login?error=email_provider_not_allowed`). Accepted: Gmail, Outlook, iCloud, or a work/school email.
- Via GitHub, the GitHub account's PRIMARY email is what counts: a GitHub account registered with Proton is rejected even though the OAuth authorization itself succeeds.
- The CLI login wait window is short (tens of minutes): start `freebuff login`, get the URL, and complete the web authorization immediately. The CLI may also auto-update itself between runs (observed 0.2.34 → 0.2.35).
- Region tiers: full mode in ~25+ countries; elsewhere or when flagged as VPN/proxy, a limited mode with fewer daily hours and smaller models. A datacenter exit IP may be flagged — only a real login settles which tier you get.
