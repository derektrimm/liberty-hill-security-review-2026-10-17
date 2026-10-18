# Windows laptop lab record

Status at 2026-10-18 19:27 UTC: the owner's laptop is reachable and Windows setup is progressing in the disposable VM. Sandboxie has not yet been installed. No launcher or website code has executed, and runtime containment remains **unverified**. This is an interim record, not a completed runtime assessment.

## Completed work

- The official launcher 6.17.62 installer and extracted main executable retained their recorded hashes after transfer. Windows `Get-AuthenticodeSignature` returned `Valid` for both, identifying Liberty Hill Studios LLC and a Microsoft timestamp signer. Fresh online revocation retrieval was not independently attested.
- A static inventory recorded 38 packaged native executables and libraries, including their hashes, available version resources and certificate chains. An offline verifier accepted 71 embedded signatures with strict timestamp verification. This does not establish advisory reachability or fresh revocation status.
- VirtualBox 7.2.20 build 175154 came from Oracle's official distribution. Its published SHA-256 matched and Windows reported its Oracle signature valid. USB and bridged/host-only network driver features were not requested.
- The current VM has 8 GiB RAM, three virtual CPUs, Secure Boot and an emulated TPM. Its PIIX3 configuration exposes eight network-adapter slots; all eight are `none`. The initial ICH9 configuration exposed 36 slots, also detached.
- Shared folders, clipboard including file transfers, drag/drop, USB controllers, PCI passthrough, remote display, audio, serial and parallel ports were disabled. Nested virtualization and 3D acceleration were disabled. Configuration was rechecked after changing the chipset.
- Sandboxie Plus 1.18.8 was acquired from its official release. Its release digest matched and Windows reported its signature valid. Installation is pending Windows setup completion.
- Only guest-specific random installation credentials were generated. No personal account, live target token, SSH key or publishing credential was copied into the guest.

Configuration inspection does not establish that isolation works. Guest-side network checks, Sandboxie file/registry canaries, reduced-rights checks and target execution gates must pass before running the application. No online guest networking has been enabled.

## Windows startup results

| Attempt | Guest configuration | Observed result |
| --- | --- | --- |
| 1 | 26H2 evaluation, ICH9, four virtual CPUs, default paravirtualization | Windows stopped during initialization with bug check `0x5C`, `HAL_INITIALIZATION_FAILED`. |
| 2 | Same media, ICH9, four CPUs, paravirtualization `none` | Startup did not reach installation during observation; the guest disk remained empty. |
| 3 | Same media, ICH9, three CPUs, paravirtualization `none` | The start command was interrupted by loss of laptop connectivity. On reconnection, the VM was powered off. The interruption's cause is unknown. |
| 4 | Same media, ICH9, three CPUs, paravirtualization `none` | Startup did not reach installation during observation. |
| 5 | Same media, PIIX3, four CPUs, default paravirtualization | Guest kernel and storage initialization appeared in the log, but no installed OS was established before switching evaluation media. |
| 6 | LTSC 2024 evaluation, PIIX3, four CPUs, default paravirtualization | Guest kernel and storage initialized; no installation progress was established during this attempt. |
| 7 | LTSC 2024 evaluation, PIIX3, one CPU | Windows Setup refused the configuration's system requirements. No requirement bypass was used. |
| 8 | LTSC 2024 evaluation, PIIX3, three CPUs, default paravirtualization | Windows Setup began installing and the virtual disk grew. Installation is still in progress at this record's timestamp. |

These are lab startup observations, not launcher defects. No cause is established for the earlier laptop connectivity loss. Host virtualization-based security and other protections were not weakened, and the host was not rebooted.

## Media identity

| Official input | SHA-256 | Verification |
| --- | --- | --- |
| VirtualBox 7.2.20 Windows installer | `a81777d2b36380ce042a29e9c554cf032eb46a793f62e3cc82e7411e535c2c26` | Oracle published checksum and native signature |
| Windows 11 Enterprise Evaluation 26H2 x64 English ISO | `bc3f24086ebadc94489066b5ad78089e2cf5c3491e90e790bb81a2b199c10e38` | Microsoft published checksum |
| Windows 11 Enterprise LTSC 2024 evaluation, build 26100.1742, x64 English ISO | `67cec5865eaa037a72ddc633a717a10a2bed50778862267223ddb9c60ef5da68` | Official Microsoft download; locally measured hash. Independent vendor checksum comparison unavailable. |
| Sandboxie Plus 1.18.8 x64 installer | `f27078ff74a07906fd51476079e1a7a8f5e20c8bb75a9d2ae86169d47179ae76` | Official release digest and native signature |

Acquisition references: [Oracle downloads](https://download.virtualbox.org/virtualbox/7.2.20/), [Microsoft evaluation media](https://www.microsoft.com/en-us/evalcenter/download-windows-11-enterprise), and [Sandboxie Plus 1.18.8](https://github.com/sandboxie-plus/Sandboxie/releases/tag/v1.18.8). Microsoft's [bug check reference](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/bug-check-0x5c--hal-initialization-failed) describes `0x5C`; it does not diagnose this host.

## Pending validation and disposal

Every dynamic security check remains untested. Prepared private checks cover update integrity, Windows file placement, IPC, credentials, local listeners, authentication transactions, pairing and session revocation. Prepared checks are not results. No target account or session has been created. The VM and lab files remain in use for setup; disposal has not occurred. Private evidence and test inputs remain outside this public repository. No sandbox guarantees safety.
