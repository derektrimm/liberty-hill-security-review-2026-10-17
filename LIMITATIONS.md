# Coverage and limitations

| Area | Work completed | Untested or unavailable |
| --- | --- | --- |
| Official installer | Download, hashes, archive structure, release-code comparison, offline signatures, native Windows installer and main executable signature results `Valid` | Install/uninstall behavior, independently attested fresh revocation retrieval, Store-delivered artifact identity |
| Electron isolation and IPC | Main window, game and site-pane settings, privileged sender checks and preload API review | Renderer escape, hostile frame behavior, permission prompts, sandbox effectiveness |
| Updates and file placement | Signed metadata, file hashes, path validation and update handoff review | Tampered-update execution, rollback/freeze scenarios, Windows path and reparse-point cases, extraction failures |
| Credential storage | OS-backed encryption and failure handling reviewed | Windows DPAPI behavior, filesystem ACLs, process-memory handling, offline sign-out lifecycle |
| Child processes and listeners | Selected launch arguments, environment filtering, loopback and HTTP boundary review | Actual process tree, socket exposure, firewall behavior, egress and cross-origin validation |
| OAuth and OpenID | Redirects, state, provider exchange, identity linking and protocol-specific replay review | Owned-account flow execution, account-switch scenarios, provider configuration, provider-side enforcement |
| Sessions and pairing | Token creation, expiration, proof verification, consumption, revocation and ownership checks | Replay races, logout/revocation end to end, recovery and concurrent requests |
| Server permissions | Shared auth gates and selected device/build/session ownership paths | Exhaustive role/object matrix, every API route, deployed configuration and databases |
| Website | Two anonymous response/header samples | Authenticated pages, browser runtime, complete TLS configuration, comprehensive XSS/CSRF/SSRF testing |
| Dependencies | Four-lockfile inventory and advisory correlation; 38-file native PE hash/version/signature inventory | Deployed SBOM, complete vendor dependency provenance, native advisory reachability, actual exploit reachability |

## Blocked checks

All target execution and invasive validation are currently **untested**, not passed. Windows setup is progressing in the disposable VM, but guest readiness, Sandboxie installation and containment canaries are not yet verified. No target test account or runnable staging service has been created. Provider endpoints were not attacked, replayed or used for account automation. An official dependency checksum endpoint returned HTTP 403; that independent checksum check is unverified and the restriction was not bypassed. Checks requiring provider behavior remain untested.

No benchmark, antivirus scan, penetration-test score, or clean bill of health is claimed. A valid signature authenticates bytes and publisher identity; it does not establish that those bytes are harmless. The report applies to the recorded artifacts and observation times, not later releases.

## Closeout

No target test accounts, target sessions, OAuth grants or pairing tokens have been created. There are no target test sessions to revoke. The disposable VM, evaluation media and guest-only installation credentials remain in use on the Windows laptop. **Lab disposal is pending.** The guest is running Windows setup; Sandboxie installation is pending. Target inputs have not executed. Existing personal sessions, source checkouts and release archives were preserved. Host security protections were not disabled. Public and private evidence are kept separately. GitHub publication uses the trusted host session outside the lab.
