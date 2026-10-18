# Methods

## Acquisition and identity

The source snapshot was pinned to a fetched repository commit. A newer source revision and the release corresponding to installer 6.17.62 were distinguished throughout the private review. The working checkout was not changed.

Live collection used ordinary anonymous HTTPS GET requests for the homepage, login page, public update metadata, Store listing, and one pinned official installer. Redirects were limited to HTTPS and certificate verification remained enabled. There was no crawling, port scanning, fuzzing, credential guessing, exploit traffic, or state-changing request to the target. No rate-limit or degradation response was observed in these acquisitions. A stop condition was used for rate-limit or server-failure responses.

The installer was read as data. Its embedded application archive and main executable were inspected with static tools. No installer, launcher, project script, dependency lifecycle hook, test suite, launcher child process, or downloaded game was executed. The packaged code comparison covered 46 CommonJS files and one ES module, plus two matching JSON files. Packaged metadata had the expected build-time reduction; a generated public-key record matched the source pin. Bundled products and compiled UI assets were not fully reproduced from source.

SHA-256 fingerprints identify collected artifacts. Ed25519 verification checked the signed update metadata. Authenticode verification checked file digests, signatures, certificate chains, and strict timestamp countersignatures using an offline verifier. Native Windows trust-policy checks and online revocation checks were not performed.

## Static review

The review followed selected security-relevant paths through renderer settings, preload APIs, IPC handlers, navigation, credentials, updates, file placement, subprocess startup, local HTTP handling, authentication, pairing, session revocation, and server-side ownership checks. Pattern searches located code; findings relied on reading the relevant implementation. This was a focused review, not a line-by-line audit of the entire repository.

Four lockfiles supplied a dependency inventory. Only public registry package names and versions were submitted to the [OSV API](https://google.github.io/osv.dev/api/). No private source, lockfile, credential, or private package name was submitted. Advisory matches were separated from runtime reachability, and priority runtime advisories were checked against maintainer publications. Embedded native libraries, bundled games, vendored code, and operating-system packages are not covered by this inventory.

## Execution boundary

A disposable Windows VM containing Sandboxie Plus could not be verified. Target execution stopped at that boundary. No shared build guest was substituted. The browser was used to display official documentation and this report, without signing into the target or executing its application in a personal browser.

Any continuation requires an offline disposable Windows guest, Sandboxie Plus inside it, disabled sharing/clipboard/device passthrough, and measured containment. Before network access, enforce denial of host, LAN, VPN, metadata-service, and other non-approved destinations outside the guest's control, including IPv6 and DNS-rebinding cases. Use synthetic data and owned test accounts. A sandbox does not guarantee safety.
