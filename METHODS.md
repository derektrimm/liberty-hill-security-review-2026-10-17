# Methods

## Acquisition and identity

The source snapshot was pinned to a fetched repository commit. A newer source revision and the release corresponding to installer 6.17.62 were distinguished throughout the private review. The working checkout was not changed.

Live collection used ordinary anonymous HTTPS GET requests for the homepage, login page, public update metadata, Store listing, and one pinned official installer. Redirects were limited to HTTPS and certificate verification remained enabled. There was no crawling, port scanning, fuzzing, credential guessing, exploit traffic, or state-changing request to the target. No rate-limit or degradation response was observed in these acquisitions. A stop condition was used for rate-limit or server-failure responses.

The installer was first read as data. Its embedded application archive and main executable were inspected with static tools. Later target execution occurred only inside the offline Windows guest under Sandboxie, after containment checks passed. No target code ran on the trusted host. The packaged code comparison covered 46 CommonJS files and one ES module, plus two matching JSON files. Packaged metadata had the expected build-time reduction; a generated public-key record matched the source pin. Bundled products and compiled UI assets were not fully reproduced from source.

SHA-256 fingerprints identify collected artifacts. Ed25519 verification checked the signed update metadata. Authenticode verification checked file digests, signatures, certificate chains, and strict timestamp countersignatures using an offline verifier. A later static `Get-AuthenticodeSignature` check on the owner's trusted Windows laptop returned `Valid` for the official installer, with Liberty Hill Studios LLC as signer and a Microsoft timestamp signer. This did not execute the installer. Fresh online revocation retrieval was not independently attested. The later native check for the extracted main executable also returned `Valid`. A 38-file native inventory recorded hashes and available version resources, with 71 embedded signatures verified offline under strict timestamp checks.

## Static review

The review followed selected security-relevant paths through renderer settings, preload APIs, IPC handlers, navigation, credentials, updates, file placement, subprocess startup, local HTTP handling, authentication, pairing, session revocation, and server-side ownership checks. Pattern searches located code; findings relied on reading the relevant implementation. This was a focused review, not a line-by-line audit of the entire repository.

Four lockfiles supplied a dependency inventory. Only public registry package names and versions were submitted to the [OSV API](https://google.github.io/osv.dev/api/). No private source, lockfile, credential, or private package name was submitted. Advisory matches were separated from runtime reachability, and priority runtime advisories were checked against maintainer publications. Native PE identity and signatures are recorded separately. Complete native advisory reachability, bundled-game and operating-system dependency coverage remain unavailable.

## Execution boundary

The laptop's disposable VirtualBox guest did not finish Windows setup. No target ran there. A separate Windows 11 Enterprise LTSC 2024 evaluation guest was installed under QEMU/KVM, with Sandboxie Plus 1.18.8 inside it. The initial laptop setup and successful fallback are recorded in [the lab record](LAB-VALIDATION.md).

The KVM guest had no virtual network adapter, USB controller, shared folder, clipboard integration, device passthrough or guest agent. Its host process ran without capabilities, under seccomp and a separate network/mount namespace with no host home directory or external network route. Guest checks confirmed Secure Boot, TPM, no hardware network adapters, no default route and no mapped shares. Sandboxie canaries verified file and registry virtualization, dropped administrator rights and the injected Sandboxie module before target execution. Repeated tests used separately verified boxes. These checks establish the observed boundary, not a safety guarantee.

The guest remained offline. Read-only optical images carried verified inputs; bounded output-only serial records carried allowlisted reports with byte lengths and SHA-256 hashes. The visible console used authenticated Unix sockets through a loopback-only tunnel, with clipboard transfer disabled. Personal accounts, secrets, publishing credentials and real-user data stayed outside the guest.

## Runtime method

Launcher checks used byte-verified packaged modules and the signed executable. Website checks used pinned source, synthetic databases, synthetic accounts and local provider doubles. External notifications and selected audit/avatar side effects were inert fixtures. No test contacted a provider or live target. Node major 22 matched the website's source container declaration, but the Windows fixture is not the deployed Linux image.

Positive controls and deliberate guard removals distinguish a functioning check from a test that always reports success. Product-source mutations were confined to disposable fixture copies and restored after the negative-control run. Failed fixture setup, missing resources, launch/output-capture failures and incomplete checks remain in the private evidence; they are not classified as product vulnerabilities. Final coverage records only checks that produced reviewed results.

Provider restrictions were respected. Blocked documentation and independent dependency-checksum requests were not bypassed. Real-provider enforcement, deployed configuration and online egress-policy checks remain untested. Any future online run requires externally enforced denial of host, LAN, VPN, metadata and other disallowed destinations, including IPv6 and DNS changes.
