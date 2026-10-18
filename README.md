# Liberty Hill Studios security review

Owner-authorized review of the launcher and website, performed October 17-18, 2026. Static analysis and passive live inspection were followed by offline validation in a disposable Windows VM with Sandboxie Plus.

**Status: the focused review and offline validation are complete. Synthetic sessions were retired, both disposable labs were discarded, and the task-installed laptop hypervisor was removed. Findings remain open. This is not a security certification.**

The official installer was **6.17.62**. Its hash matched the signed update feed; installer and main-executable signatures verified. Forty-seven packaged code files matched the corresponding release source. Native execution confirmed Electron **44.4.5**, Chromium **152.0.7977.130** and embedded Node **24.21.0**. Artifact identity does not establish safe behavior.

The review confirmed an authentication transaction-binding weakness in a local synthetic fixture and a bounded Windows filename-validation gap. Dependency advisory matches, report-only CSP, missing PKCE and Electron hardening settings also require follow-up. No attacker account takeover, remote code execution, sandbox escape or real-user access was demonstrated.

Runtime evidence includes 17 passed launcher module groups, six passed native Electron groups, and 38 completed website baseline cases. One website case confirms the transaction-binding behavior rather than a protective control. Two deliberately removed security guards caused the intended failures; restored suites passed. Counts describe this selected coverage, not an overall security score.

| Report | Contents |
| --- | --- |
| [Findings](FINDINGS.md) | Confirmed observations, bounded flaws and unproven impact |
| [Methods](METHODS.md) | Collection, containment, fixtures and controls |
| [Coverage and limitations](LIMITATIONS.md) | Tested boundaries and explicitly untested areas |
| [Evidence](EVIDENCE.json) | Artifact identity and sanitized result fingerprints |
| [Windows lab](LAB-VALIDATION.md) | Failed laptop setup, successful offline fallback and disposal |
| [Disclosure](SECURITY.md) | Handling of private technical details |

Scope entry points: [Microsoft Store listing](https://apps.microsoft.com/detail/XP9MNT3Z852FML?mode=direct) and [studio website](https://libertyhillstudio.com/).

The installer came from the official studio download. Exact Store-delivered bytes and the website's deployed image were not attested. The guest never had network access. Provider behavior, online egress policies and comprehensive live exploitation remain untested. Private source, binaries, credentials, raw logs and actionable reproduction details are excluded from this repository.
