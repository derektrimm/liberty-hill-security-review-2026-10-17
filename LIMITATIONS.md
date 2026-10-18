# Coverage and limitations

| Area | Completed work | Explicitly untested or unavailable |
| --- | --- | --- |
| Official installer | Hashes, signatures, release comparison, boxed installation and launch; complete uninstall observed after descendant exit | Exact Store artifact, independently attested fresh revocation, all Windows versions |
| Electron isolation and IPC | Source review, 50-handler synthetic sender checks, native authorized/foreign renderer checks and actual application composition | Renderer exploit or escape, every pane/permission/frame combination |
| Updates and placement | Signed feed acceptance, tamper/platform/version-selection refusal, local download integrity, Windows path and CAS checks | Real online updater/install chain, freeze prevention, reparse-point race, Mac ZIP extraction |
| Credentials | Native protected storage write/read/restart, corrupt data, unavailable encryption and sign-out behavior | Cross-user ACL attack, process-memory extraction, real provider/server revocation |
| Processes and listeners | Environment filtering; sampled boxed process identity and IPv4 loopback bind; native cross-origin read refusal | Exhaustive child trees, games/vendor processes, public-site browser policies and DNS rebinding |
| OAuth/OpenID | Local actual-route tests for state, redirects, context switching, identity conflicts and logout; Steam verifier tests | Real provider configuration/enforcement, provider replay, live account linking, end-to-end PKCE implementation |
| Sessions and pairing | Token integrity/purpose/expiry, revocation, proof, single-use concurrency, cross-account checks, role/suspension changes | Every route/object/role combination, exhaustive merge graph and production concurrency |
| Website | Pinned source tests and two passive live header samples | Deployed image attestation, authenticated live pages, comprehensive TLS/XSS/CSRF/SSRF testing |
| Dependencies | Four-lockfile advisory correlation, 38 native PE files and 71 embedded offline signatures | Deployed SBOM, complete native/vendor provenance and advisory exploitability |

## Scope of successful tests

The website ran on Windows Node 22.23.3, matching the source container's major version, with synthetic SQLite databases and local provider/cookie fixtures. It was not the deployed Linux image or a full browser-to-provider flow. All 167 source migrations were applied in the full-schema fixtures. The generated Prisma client and Windows engine have a separate provenance limitation: the independent vendor checksum request returned HTTP 403 and was not bypassed.

Launcher module tests used Node 24.22.0; native tests used the signed executable's Electron 44.4.5, Chromium 152.0.7977.130 and Node 24.21.0. Native fixture entry points exercised unchanged packaged code. One composition test excludes the ordinary main bootstrap and Discord presence. The separate official installation/launch observation is narrower than a full authenticated product playthrough.

The junction fixture could not establish its prerequisite under Sandboxie. It is **untested**, not passed. Initial fixture failures, missing resources, output-capture and process-lifecycle problems were retained and corrected; successful reruns supersede those harness failures only for the stated checks.

## Restrictions

Guest networking was never enabled. Therefore no online egress-policy, host/LAN/VPN reachability, DNS-rebinding or provider-facing validation is claimed. Provider protection blocks and a checksum HTTP 403 were respected. No real-user access, credential guessing, brute force, destructive production change or attack on a provider occurred. No rate-limit or service-degradation response was observed during the low-rate passive collection.

Signatures authenticate bytes and publisher identity, not harmlessness. No antivirus verdict, benchmark, security score, exhaustive audit or safety guarantee is claimed. Results apply to the recorded artifacts and fixture conditions.

## Closeout

Synthetic session and device credentials were retired by fixture cleanup; all three Sandboxie boxes passed a final retirement sweep. No personal or provider account was used. Both disposable VMs, their guest credentials and lab directories were discarded after evidence export. The task-installed laptop VirtualBox package was removed; the pre-existing KVM installation and personal sessions were preserved. Public publication occurred from the trusted Linux session outside the lab. Deletion is logical disposal, not an attestation of forensic media erasure.
