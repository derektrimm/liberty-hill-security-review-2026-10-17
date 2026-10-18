# Coverage and limitations

| Area | Work completed | Untested or unavailable |
| --- | --- | --- |
| Official installer | Download, hashes, archive structure, release-code comparison, offline signatures | Install/uninstall behavior, native Windows trust and revocation, Store-delivered artifact identity |
| Electron isolation and IPC | Main window, game and site-pane settings, privileged sender checks and preload API review | Renderer escape, hostile frame behavior, permission prompts, sandbox effectiveness |
| Updates and file placement | Signed metadata, file hashes, path validation and update handoff review | Tampered-update execution, rollback/freeze scenarios, Windows path and reparse-point cases, extraction failures |
| Credential storage | OS-backed encryption and failure handling reviewed | Windows DPAPI behavior, filesystem ACLs, process-memory handling, offline sign-out lifecycle |
| Child processes and listeners | Selected launch arguments, environment filtering, loopback and HTTP boundary review | Actual process tree, socket exposure, firewall behavior, egress and cross-origin validation |
| OAuth and OpenID | Redirects, state, provider exchange, identity linking and protocol-specific replay review | Owned-account flow execution, account-switch scenarios, provider configuration, provider-side enforcement |
| Sessions and pairing | Token creation, expiration, proof verification, consumption, revocation and ownership checks | Replay races, logout/revocation end to end, recovery and concurrent requests |
| Server permissions | Shared auth gates and selected device/build/session ownership paths | Exhaustive role/object matrix, every API route, deployed configuration and databases |
| Website | Two anonymous response/header samples | Authenticated pages, browser runtime, complete TLS configuration, comprehensive XSS/CSRF/SSRF testing |
| Dependencies | Four-lockfile inventory and advisory correlation | Deployed SBOM, all vendor/native dependencies, actual exploit reachability |

## Blocked checks

All target execution and invasive validation are marked **untested**, not passed. No approved disposable staging copy or test accounts were provisioned. Provider endpoints were not attacked, replayed, or used for account automation. Checks requiring provider behavior remain untested rather than being worked around.

No benchmark, antivirus scan, penetration-test score, or clean bill of health is claimed. A valid signature authenticates bytes and publisher identity; it does not establish that those bytes are harmless. The report applies to the recorded artifacts and observation times, not later releases.

## Closeout

No test accounts, target sessions, OAuth grants, pairing tokens, lab VM, or Sandboxie container were created. There were therefore no test sessions to revoke and no lab to discard. Existing user sessions, credentials, services, source checkouts, and release archives were left in place. Reviewed public and private report exports were retained separately. GitHub publication used the trusted host session outside any lab.
