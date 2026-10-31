# Pxxl login limits (observed 2026-10-31)

- First attempt from a shared browser environment: OAuth with GitHub succeeds, then Pxxl's callback fails with the explicit error "Authentication Failed — Maximum number of accounts per device reached".
- A brand-new browser profile got past that message (GitHub login + device verification passed), but the Pxxl callback then silently bounced back to the login page three times with no error text and no session.
- Conclusion: Pxxl applies device/account restrictions that are not fully surfaced in the UI. Retrying in the same environment does not help. Options: use a genuinely different device, wait, or contact Pxxl support.
- The deployment itself was never reached; repo and env-var layout were ready (Node project, `npm start`, env vars only on the Pxxl side, no Docker — Docker/Drop are paid-locked on Free).
- Status: parked by choice; working backups (InstaBox + Zoho) cover the need.
