# Windows lab record

The offline runtime review completed on October 18, 2026 UTC. Both disposable labs were discarded after reviewed evidence export. No sandbox guarantees safety.

## Laptop attempt

The authorized laptop was reachable and supplied native signature validation. A disposable VirtualBox 7.2.20 guest used official Windows evaluation media, no network adapters, and disabled sharing, clipboard, drag/drop, USB/PCI passthrough and audio. Earlier 26H2 attempts failed or stalled; an LTSC 2024 attempt installed to disk but remained at 42 percent in its later setup phase. No target code executed on the laptop. No cause was established for the startup failures. Host security protections were not disabled and the host was not rebooted.

The incomplete guest was paused while a separate KVM guest was prepared. After evidence export, the laptop VM, disk and lab files were deleted. The task-installed VirtualBox package was then removed with exit code zero, no remaining executable/package registration, and no reboot requested. No pre-existing VM was removed.

## Successful offline Windows guest

- QEMU 11.1.2 with KVM, two virtual CPUs, 6 GiB memory and a disposable 64 GiB virtual disk.
- Windows 11 Enterprise LTSC 2024 evaluation, build 26100.1742. Guest checks confirmed Secure Boot and a ready TPM. Firmware revocation-list freshness was not independently attested.
- Sandboxie Plus 1.18.8 with 5.73.8 driver/service components. Native signature checks returned Valid for the inspected installed components.
- No guest network adapter, shared folder, clipboard integration, USB controller, device passthrough, audio or guest agent. No personal account, production secret or publishing credential entered the guest.
- QEMU ran in separate mount/network namespaces, without capabilities, with seccomp and no host home directory or external route. Host checks passed before guest continuation.
- Guest checks found no hardware network adapter, default route or mapped share. Sandboxie file/registry virtualization, dropped administrator rights and injected-module canaries passed before execution and again for fresh test boxes.
- Inputs arrived on read-only optical media. Allowlisted reports left through an output-only serial log with checked sizes and SHA-256 hashes. An authenticated console was visible in the browser; clipboard transfer was disabled.

## Reviewed outcomes

| Group | Result |
| --- | --- |
| Packaged launcher modules | 17 groups passed, two bounded behaviors observed, one junction prerequisite unavailable |
| Native Electron fixtures | Six groups passed; offline sign-out retention observed |
| Website baseline | 38 cases completed: 37 protective-control cases and one account-context-switch observation |
| Negative controls | Removed revocation/proof guards caused intended failures; restored suites passed |
| Official installer | Reviewed executable and archive hashes matched after boxed installation; launcher process and loopback listener observed |
| Uninstall | Child completion awaited; executable and application archive absent in the sandboxed view |
| Retirement | All three boxes verified clean of retained synthetic credentials and fixture database directories |

Early runs exposed test-harness problems: an obsolete VM-name assertion, missing theme resource, missing migration bookkeeping, read-only fixture replacement, GUI-tool output capture and premature process-lifecycle observations. These were corrected without changing production source or weakening containment. Failed attempts remain in private evidence and are not product findings.

## Disposal

The KVM guest was shut down and its service stopped after reviewed evidence export. Its virtual disk, TPM state, guest credentials and lab directory were deleted. Temporary console/tunnel services and local credential-bearing media were removed. The existing hypervisor installation was preserved. No online guest networking was enabled at any point. Logical deletion does not imply forensic secure erasure.

## Media identity

| Official input | SHA-256 | Verification |
| --- | --- | --- |
| VirtualBox 7.2.20 Windows installer | `a81777d2b36380ce042a29e9c554cf032eb46a793f62e3cc82e7411e535c2c26` | Oracle published checksum and native signature |
| Windows 11 Enterprise Evaluation 26H2 x64 English ISO | `bc3f24086ebadc94489066b5ad78089e2cf5c3491e90e790bb81a2b199c10e38` | Microsoft published checksum |
| Windows 11 Enterprise LTSC 2024 evaluation, build 26100.1742, x64 English ISO | `67cec5865eaa037a72ddc633a717a10a2bed50778862267223ddb9c60ef5da68` | Official Microsoft download; locally measured hash. Independent vendor checksum comparison unavailable. |
| Sandboxie Plus 1.18.8 x64 installer | `f27078ff74a07906fd51476079e1a7a8f5e20c8bb75a9d2ae86169d47179ae76` | Official release digest and native signature |

Acquisition references: [Oracle downloads](https://download.virtualbox.org/virtualbox/7.2.20/), [Microsoft evaluation media](https://www.microsoft.com/en-us/evalcenter/download-windows-11-enterprise), and [Sandboxie Plus 1.18.8](https://github.com/sandboxie-plus/Sandboxie/releases/tag/v1.18.8). Microsoft's [bug check reference](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/bug-check-0x5c--hal-initialization-failed) describes `0x5C`; it does not diagnose this host.
