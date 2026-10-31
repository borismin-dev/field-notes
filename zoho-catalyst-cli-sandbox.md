# Zoho Catalyst CLI in a restricted sandbox

Problem: `zcatalyst-cli` device-code login never completes in a root-run, restricted-FS sandbox.

What was wrong and the fixes:
1. The device-code poller gives up after ~30 polls (~70 s), but the code lives ~5 min and the human needs time to authorize. Patch `login.js`: raise the poll limit (30 → 900).
2. The `atomically` fs helper only swallows EPERM for non-root users; this sandbox returns EPERM on chown even for root. Patch `fs_handlers.js` to swallow EPERM regardless of uid.
3. Interactive error-reporting prompts hang non-interactive runs. Set `ZCATALYST_NON_INTERACTIVE=1`.

Flow that works: `catalyst login --no-localhost --dc us`, open the browser FIRST, then generate the code and hand it over immediately (codes live ~5 min) at accounts.zoho.com/oauth/v3/device.

Lesson: generate the device code only when the authorizing browser is already open and ready.
