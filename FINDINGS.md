# Findings

Confirmed facts and locally reproduced behavior are separated from unproven exploitability. Priorities guide owner follow-up; no CVSS score or claim of remote compromise is assigned without evidence.

## Confirmed observations and bounded flaws

| ID | Result | Evidence and limitation | Recommended action |
| --- | --- | --- | --- |
| C-01 | Dependency versions match published advisories | 48 distinct advisory records across 20 package/version pairs. Some concern build tooling or unused features. Deployed reachability is untested. | Prioritize actual runtime and image-processing dependencies, verify deployed inventory and update affected components in staging. |
| C-02 | Sampled website CSP is report-only | Two anonymous pages had no enforcing CSP header or meta policy. Other security headers were present. No XSS was demonstrated. | Stage and test an enforcing policy with narrower script permissions. |
| C-03 | Reviewed confidential OAuth code flow lacks PKCE | State and client authentication are present. Provider configuration and a code-injection attack were not tested. | Add S256 PKCE where supported and preserve transaction binding and state checks. |
| C-04 | Shipped Electron package retains optional hardening gaps | Static fuse inspection found package-integrity protections disabled and development capabilities enabled. This is not standalone RCE. | Audit required capabilities, apply compatible fuse protections before signing, and retest the resulting artifact. |
| C-05 | Authentication transaction can complete under a different account context | Actual application routes and database code reproduced the context mismatch with synthetic accounts and a local provider double. Previously tracked as S-01. Attacker feasibility and real-provider behavior remain untested. | Bind pending transactions to their initiating context and intent; retire them on relevant session changes and reject mismatches. |
| C-06 | Windows filename policy permits nonordinary filesystem semantics | A packaged path helper accepted a synthetic Windows filename case outside an ordinary-file policy. Remote delivery, signed-content abuse and a full installation exploit were not demonstrated. | Define and enforce the intended Windows filename policy and verify it through the real placement path in staging. |

C-01 needs prompt private exposure triage. C-05 deserves transaction-binding remediation and retesting. C-06 is a bounded validation gap; C-02 through C-04 are hardening work with unproven exploit impact. Detailed source locations and reproduction material remain private.

[Electron security guidance](https://www.electronjs.org/docs/latest/tutorial/security) and [fuse documentation](https://www.electronjs.org/docs/latest/tutorial/fuses) describe the package protections. [RFC 9700](https://www.rfc-editor.org/rfc/rfc9700.html) recommends PKCE for confidential code clients; [Discord's OAuth documentation](https://docs.discord.com/developers/topics/oauth2) also recommends code flow with PKCE. [MDN's report-only CSP reference](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Content-Security-Policy-Report-Only) explains its non-enforcing behavior.

## Suspicion with narrowed impact

**S-02: local discovery boundary.** A synthetic foreign-authority/origin request received limited discovery metadata without CORS read permission. A native Chromium positive-control test confirmed that another loopback origin could not read that response. No credential disclosure was demonstrated. Public-site browser behavior, DNS rebinding and broader reachability remain untested. Validate authority before dispatch and minimize metadata.

## Other observed behavior

Offline sign-out reported failure and retained the protected credential. With a synthetic server acknowledgement, sign-out cleared it. This is a confirmed lifecycle behavior, not evidence that real-server revocation failed. Product messaging and recovery should clearly distinguish unsuccessful sign-out from a completed one.

## Controls validated within the fixture scope

- Update signature, tamper, platform, version-selection, download hash and invalid-format refusal checks passed.
- Fourteen Windows traversal/absolute-path cases were refused, and cache corruption, truncation and overflow checks passed. A junction setup could not be established under the lab restrictions and remains untested.
- Privileged IPC rejected 100 synthetic foreign/child-frame events across 50 handlers. Native Electron also refused an unrelated renderer while allowing its positive control. The actual application composition retained renderer isolation and a loopback listener.
- Native protected storage, restoration, corrupt-data handling and acknowledged sign-out checks passed. Unavailable encryption failed closed in a separate module fixture.
- Website state mismatch, return destinations, identity conflicts, email non-linking, logout, pairing proof, single-use concurrency, ownership, revocation and selected live permission checks passed. The account-context case instead established C-05.
- Removing the actual session-revocation and pairing-proof guards caused the intended assertions to fail. Restoring each source file restored passing results.

Steam uses OpenID 2.0, not OpenID Connect. Direct verification delegates replay rejection to the provider under [OpenID 2.0 section 11.3](https://openid.net/specs/openid-authentication-2_0.html#verify_nonce). Local verifier checks passed; provider replay enforcement was not tested.
