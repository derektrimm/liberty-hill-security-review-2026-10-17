# Methods

## Acquisition and identity

The source snapshot was pinned to a fetched repository commit. A newer source revision and the release corresponding to installer 6.17.62 were distinguished throughout the private review. The working checkout was not changed.

Live collection used ordinary anonymous HTTPS GET requests for the homepage, login page, public update metadata, Store listing, and one pinned official installer. Redirects were limited to HTTPS and certificate verification remained enabled. There was no crawling, port scanning, fuzzing, credential guessing, exploit traffic, or state-changing request to the target. No rate-limit or degradation response was observed in these acquisitions. A stop condition was used for rate-limit or server-failure responses.

The installer was read as data. Its embedded application archive and main executable were inspected with static tools. No installer, launcher, project script, dependency lifecycle hook, test suite, launcher child process, or downloaded game was executed. The packaged code comparison covered 46 CommonJS files and one ES module, plus two matching JSON files. Packaged metadata had the expected build-time reduction; a generated public-key record matched the source pin. Bundled products and compiled UI assets were not fully reproduced from source.

SHA-256 fingerprints identify collected artifacts. Ed25519 verification checked the signed update metadata. Authenticode verification checked file digests, signatures, certificate chains, and strict timestamp countersignatures using an offline verifier. A later static `Get-AuthenticodeSignature` check on the owner's trusted Windows laptop returned `Valid` for the official installer, with Liberty Hill Studios LLC as signer and a Microsoft timestamp signer. This did not execute the installer. Fresh online revocation retrieval was not independently attested. The later native check for the extracted main executable also returned `Valid`. A 38-file native inventory recorded hashes and available version resources, with 71 embedded signatures verified offline under strict timestamp checks.

## Static review

The review followed selected security-relevant paths through renderer settings, preload APIs, IPC handlers, navigation, credentials, updates, file placement, subprocess startup, local HTTP handling, authentication, pairing, session revocation, and server-side ownership checks. Pattern searches located code; findings relied on reading the relevant implementation. This was a focused review, not a line-by-line audit of the entire repository.

Four lockfiles supplied a dependency inventory. Only public registry package names and versions were submitted to the [OSV API](https://google.github.io/osv.dev/api/). No private source, lockfile, credential, or private package name was submitted. Advisory matches were separated from runtime reachability, and priority runtime advisories were checked against maintainer publications. Native PE identity and signatures are recorded separately. Complete native advisory reachability, bundled-game and operating-system dependency coverage remain unavailable.

## Execution boundary

A new disposable VM was provisioned on the owner's Windows laptop using official Windows evaluation media and VirtualBox. All virtual network adapters are absent; shared folders, clipboard, drag/drop, USB and other device passthrough are disabled. These are recorded hypervisor settings, not a completed containment test. Earlier startup attempts failed or did not reach installation; after the laptop reconnected, LTSC 2024 evaluation setup began making progress. Guest readiness and Sandboxie containment remain pending. See [the lab record](LAB-VALIDATION.md). No personal account or publishing credential was placed in the guest. The browser displays official references, this report and reviewed VM screenshots, without signing into the target or running its application in a personal browser.

Any continuation requires an offline disposable Windows guest, Sandboxie Plus inside it, disabled sharing/clipboard/device passthrough, and measured containment. Before network access, enforce denial of host, LAN, VPN, metadata-service, and other non-approved destinations outside the guest's control, including IPv6 and DNS-rebinding cases. Use synthetic data and owned test accounts. A sandbox does not guarantee safety.
