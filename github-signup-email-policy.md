# Which emails can register a GitHub account (verified 2026-10)

- outlook.com / hotmail.com: GitHub paused NEW sign-ups with these domains in late Sep 2026 (officially: sustained coordinated fraud/abuse). Symptom is exactly "Email domain could not be verified" with the Create button disabled. Existing accounts are unaffected. No exception channel, no resumption timetable. It is a policy block, not a browser/environment fault (easy to misdiagnose).
- Disposable/temp-mail services are blocked before any code is sent.
- Custom-domain mail can pass GitHub's domain check yet never receive the launch code if the mail host drops it — observed with a Smailr-hosted domain: code "sent" twice, never arrived in inbox or spam over 24 h.
- Proton Mail works for registration; the launch code and later device-verification codes can only be read by the mailbox owner.
- Every new browser environment triggers a fresh GitHub device-verification code by email — expect one code per new profile/device, each time-limited.
- There is no published whitelist; Gmail is the most reliable in practice.
