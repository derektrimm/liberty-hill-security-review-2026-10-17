# Findings

A confirmed observation establishes the stated fact, not every possible consequence. Advisory severity belongs to the upstream package and is not automatically the severity of this deployment. Priorities below guide owner follow-up; no CVSS score is assigned without validated impact.

## Confirmed observations

| ID | Observation | Evidence and limit | Recommended action |
| --- | --- | --- | --- |
| C-01 | Dependency versions match published advisories | A static inventory query returned 48 distinct advisory records across 20 package/version pairs. Production exposure and exploitability were not established. Some matches concern build tooling or features not found in the reviewed source. | Prioritize runtime dependency triage, upgrade affected components, and verify the deployed inventory in staging. |
| C-02 | Website CSP is report-only on the two sampled pages | Normal anonymous responses contained a report-only policy and no enforcing CSP header or HTML meta policy. Other security headers were present. This is a defense gap, not evidence of XSS. | Introduce an enforcing policy through a tested rollout and reduce broad script permissions. |
| C-03 | The reviewed OAuth code flow does not use PKCE | The authorization request and token exchange lack PKCE parameters. The flow is a confidential server client with state and client authentication. No code injection or account takeover was demonstrated. | Add S256 PKCE after confirming provider support for the configured application; preserve state and bind each transaction to its initiating context. |
| C-04 | The Windows package retains default Electron hardening settings | Static binary inspection found optional package protections disabled and development-oriented capabilities enabled. Remote exploitation was not demonstrated. | Audit required runtime capabilities, disable unused ones, and enable package integrity protections before signing a new build. |

C-01 deserves the earliest private triage. C-03 is a protocol hardening improvement. C-02 and C-04 are defense-in-depth work; the evidence does not support describing them as standalone remote compromises.

[Electron's security guidance](https://www.electronjs.org/docs/latest/tutorial/security) and [fuse documentation](https://www.electronjs.org/docs/latest/tutorial/fuses) explain the relevant package protections. [RFC 9700](https://www.rfc-editor.org/rfc/rfc9700.html) recommends PKCE for confidential authorization-code clients; [Discord's OAuth documentation](https://docs.discord.com/developers/topics/oauth2) also recommends code flow with PKCE. [MDN's report-only CSP reference](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Content-Security-Policy-Report-Only) explains that this header does not enforce its policy.

## Suspicions requiring isolated validation

| ID | Area | Current conclusion |
| --- | --- | --- |
| S-01 | Authentication transaction binding | A possible mismatch between an initiated flow and the session present at completion needs controlled account-switch and replay validation. No unauthorized linking was demonstrated. |
| S-02 | Local discovery boundary | A local discovery handler warrants stricter request validation. Browser reachability and any practical information exposure remain untested. |

Private evidence describes the relevant paths and validation criteria. This repository deliberately omits request recipes, internal endpoints, payloads, and exploit chains.

## Positive controls observed

The reviewed paths include renderer isolation, restricted privileged IPC, signed and hashed launcher updates, validated build manifests, OS-backed launcher credential encryption, proof-bound pairing, and server-side account/device checks. Public redirects were not fuzzed. Controls were inspected in source; their behavior under attack remains untested.

The Steam integration uses OpenID 2.0. It is not OpenID Connect, so an OIDC ID-token checklist or an OAuth PKCE requirement cannot simply be applied to it. Its direct assertion verification delegates replay enforcement to the provider under [OpenID 2.0 section 11.3](https://openid.net/specs/openid-authentication-2_0.html#verify_nonce). Provider replay behavior was not tested.
