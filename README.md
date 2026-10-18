# Liberty Hill Studios security review

Static and passive assessment of the Liberty Hill Studios launcher and website, authorized by owner Derek Trimm on October 17, 2026. Evidence was collected on October 18 UTC, spanning October 17 and 18 in America/Chicago.

**Status: static and passive review completed within the stated scope. Windows setup is progressing in a disposable VM on the owner's laptop. Guest readiness and Sandboxie containment are still pending. Target runtime and exploit validation remain untested. This is not a security certification.**

The reviewed official Windows installer is version **6.17.62**. Its SHA-256 matches the signed update feed. Offline checks verified the feed signature and the timestamped Authenticode signatures on both the installer and its main executable. The Windows laptop returned **Valid** for native Authenticode checks on both the installer and main executable, without executing them. An extended static inventory verified 71 embedded signatures across 38 native components offline; fresh revocation retrieval was not independently attested. Forty-seven packaged application code files matched the corresponding release source byte for byte. These checks establish artifact identity and integrity, not safe behavior.

Four observations require follow-up: dependency advisory matches, a report-only website content policy, an OAuth defense missing from the reviewed flow, and unused Electron hardening controls. Two additional concerns remain unvalidated. No account takeover, remote code execution, authorization bypass, sandbox escape, or credential theft was demonstrated.

| Report | Contents |
| --- | --- |
| [Findings](FINDINGS.md) | Confirmed observations, suspicions, and priorities |
| [Methods](METHODS.md) | Evidence collection and review boundaries |
| [Coverage and limitations](LIMITATIONS.md) | What was examined and what remains untested |
| [Evidence](EVIDENCE.json) | Public artifact identity, signatures, and selected observations |
| [Windows lab](LAB-VALIDATION.md) | Laptop work, containment configuration, boot failures, and cleanup status |
| [Disclosure](SECURITY.md) | Handling of private technical details |

Scope entry points: [Microsoft Store listing](https://apps.microsoft.com/detail/XP9MNT3Z852FML?mode=direct) and [studio website](https://libertyhillstudio.com/).

The installer was downloaded from the studio's official website. The exact binary delivered by Microsoft Store was not obtained, so equivalence with that distribution channel is unverified. The website's deployed commit and production dependency inventory were not attested.

Private source, source locations, full dependency mappings, detailed validation cases, credentials, binaries, and raw logs are excluded from this repository. No workflows or deployable application code are included.
