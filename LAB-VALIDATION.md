# Windows laptop lab record

The owner's Windows laptop was used for native static signature verification and to provision a new disposable VM. No launcher or website code was executed. Runtime containment remains **unverified**.

## Completed work

- The official launcher 6.17.62 installer retained its recorded SHA-256 after transfer. Windows `Get-AuthenticodeSignature` returned `Valid`, identifying Liberty Hill Studios LLC and a Microsoft timestamp signer. Fresh online revocation retrieval was not independently attested.
- VirtualBox 7.2.20 build 175154 was installed from Oracle's official distribution. Its published SHA-256 matched and Windows reported its Oracle signature valid. USB and bridged/host-only network driver features were not requested.
- Windows 11 Enterprise Evaluation 26H2 media matched Microsoft's published SHA-256. The VM used an emulated TPM and Secure Boot.
- All 36 virtual network adapter slots were set to `none`. Shared folders, clipboard including file transfers, drag/drop, USB controllers, PCI passthrough, remote display, audio, serial and parallel ports were disabled. Nested virtualization and 3D acceleration were disabled.
- Sandboxie Plus 1.18.8 was acquired from its official release. The release digest matched and Windows reported its signature valid. It was not installed because the Windows guest did not become ready.
- Only guest-specific random installation credentials were generated. No personal account, live target token, SSH key, or publishing credential was copied into the guest.

Configuration inspection does not establish that isolation works. Guest-side network checks, Sandboxie file/registry canaries, reduced-rights checks, and target execution gates were prepared but could not run.

## Windows startup results

| Attempt | Guest configuration | Observed result |
| --- | --- | --- |
| 1 | 8 GiB RAM, 4 virtual CPUs, default paravirtualization | Windows stopped during initialization with bug check `0x5C`, `HAL_INITIALIZATION_FAILED`. |
| 2 | Same VM, paravirtualization set to `none` | Windows remained at startup. Storage counters and the empty guest disk showed no installation progress during the final observation interval. No ready guest or Guest Additions was detected. |
| 3 | Same isolated VM, 3 virtual CPUs, paravirtualization `none` | The start command was interrupted by loss of laptop connectivity. Final boot and power state are unknown. |

These are lab startup failures, not evidence of a launcher defect. No cause is established for the laptop becoming unreachable. Host security protections were not weakened to troubleshoot the VM.

## Media identity

| Official input | SHA-256 |
| --- | --- |
| VirtualBox 7.2.20 Windows installer | `a81777d2b36380ce042a29e9c554cf032eb46a793f62e3cc82e7411e535c2c26` |
| Windows 11 Enterprise Evaluation 26H2 x64 English ISO | `bc3f24086ebadc94489066b5ad78089e2cf5c3491e90e790bb81a2b199c10e38` |
| Sandboxie Plus 1.18.8 x64 installer | `f27078ff74a07906fd51476079e1a7a8f5e20c8bb75a9d2ae86169d47179ae76` |

Acquisition references: [Oracle downloads](https://download.virtualbox.org/virtualbox/7.2.20/), [Microsoft evaluation media](https://www.microsoft.com/en-us/evalcenter/download-windows-11-enterprise), and [Sandboxie Plus 1.18.8](https://github.com/sandboxie-plus/Sandboxie/releases/tag/v1.18.8). Microsoft's [bug check reference](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/bug-check-0x5c--hal-initialization-failed) describes `0x5C`; it does not diagnose this host.

## Unfinished work and disposal

Every dynamic security check remains untested. No online lab networking was enabled. No target account or session was created, so target session revocation is not applicable. **The VM and laptop lab files have not yet been verified deleted because the host is unreachable.** No completed-disposal claim is made. Private evidence and prepared checks remain outside this public repository.
