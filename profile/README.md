# SynapticChain — Zero-Trust Banking Clearinghouse

> A Layer-1 blockchain platform built around **compiler-driven static scheduling**:
> contracts in SynapticLang compile to fully resolved execution plans (lockstep,
> dependency-aware, statically scheduled) that the SynapticVM runs with parallel
> lanes — deterministic by construction. 100k+ TPS target, sub-500ms finality,
> ISO 20022 financial-message interoperability.
>
> The product is a **zero-trust banking clearinghouse**: an L1 settlement core
> (multilateral netting clearinghouse with margin custody) plus two evidence rails
> (XRPL testnet escrows, Solana devnet lane-shard program), fronted by an x402/MCP
> gateway estate that licensed AI agents trade through end-to-end.

The core monorepo (23-crate Rust L1) is private. The **public verification path**
below uses only links a judge or diligence team can reach — and if a firm requests
deeper source access, it is granted; the boundary is confidentiality, not concealment.

---

## Colosseum Radar — BankerX (submission complete, 2026-10-12)

Judges can open every surface live, no appointment needed:

- **Clearinghouse console** — [colosseum.synapticchain.xyz](https://colosseum.synapticchain.xyz) (window status, refusals, addresses, markets, proof, tools)
- **10-stage live-fire demo** — [colosseum.synapticchain.xyz/demo](https://colosseum.synapticchain.xyz/demo)
- **Continuous Atomic Netting stream** — [colosseum.synapticchain.xyz/can](https://colosseum.synapticchain.xyz/can) (400 ms evaluation cadence)
- **Institutional position brief** — [colosseum.synapticchain.xyz/brief](https://colosseum.synapticchain.xyz/brief)
- **Institutional FX terminal** — [terminal.synapticchain.xyz](https://terminal.synapticchain.xyz)
- **FINOS traderX blotter** — [traderx.synapticchain.xyz](https://traderx.synapticchain.xyz) (desk pairs wired to live corridors, PR #470 branch running)

Demo videos (pitch + product demo):

- [BankerX — Institutional Atomic Settlement (DvP/PvP) on Solana | Colosseum Radar](https://www.youtube.com/watch?v=o92UFXH7dI4)
- [BankerX — 90-Second Technical Demo | Solana DvP, Token-2022 & Continuous Netting](https://www.youtube.com/watch?v=ZMCEc2Jge4c)
- [BankerX — Institutional Atomic Settlement (DvP/PvP) on Solana Token-2022 | Colosseum Radar Pitch](https://www.youtube.com/watch?v=AeNF2AmMmSg)
- [BankerX — 90-Second Live DvP/PvP Demo: FINOS TraderX to Solana Token-2022](https://www.youtube.com/watch?v=JvqwclnxzMQ)

---

## Verification record (fresh census, 2026-10-12)

Measured on the live tree; every live receipt below was run twice unless noted.

- **>4,800 test functions/assertions platform-wide** — 3,347 Rust test functions
  across the 23-crate L1 workspace (consensus 694, synaptic-types 373, state 299,
  compiler 247, p2p 221, node 220, vm 180) plus 634 across the estate's Rust
  service programs; 178 property-test macros; 1,161 SDK test functions (Python +
  TypeScript SDKs); ~310 across gateway, terminal, and service suites.
- **Formal invariant verification (FIV v4.4): 12/12 invariants passing**; automated
  vulnerability-triage harness (SVAH v1.0).
- **FINOS Open Source Maturity Model: Level 5 (highest tier), Grade A+, 24/24.**

| Suite | Score |
|---|---|
| Colosseum app preflight (edge-mode, strict TLS) | 21 PASS / 0 FAIL ×2 |
| finITe — FINOS conformance suite vs our agent | 131/132 ×2 |
| Interledger devnet E2E (two-ledger loop) | 13/13 ×2 |
| FDC3 StartPayment → clearinghouse bridge | 15/15 ×2 |
| R15 MCP m2m corridors | 81/81 ×2 |
| R15 watermark rolling settlement | 24/24 ×2 |
| R13 multi-rail (Solana + XRPL mixed) phase 10 | 14/14 ×2 |
| Corridor 17 (sUSD/cTZS) | 24/24 ×2 |
| Stripe-compatible card-rail shim (honest-core :8092) | E2E ×2 GREEN, F1–F9 closed, spend-cap 9/9 ×2 |
| 10-stage live wire loop (FDC3 intent → netting → dual-rail evidence → margin settlement → finalize → same-UETR pacs.008 render) | ALL 11 stages GREEN ×2 (2026-10-12) |
| Uhuru/UTA audit battery | 17/17 ×2; verdict PASS-WITH-NOTES |

Stated plainly, per estate law: the Tier-0 external audit is scoped and packaged
but **not yet executed** by an external third party. Every address in our
repositories is live-read from the mesh, never fabricated; refusals are rendered
verbatim; write transactions are never trusted without an on-ledger readback.

---

## Public repositories

**Financial rails and integration**

| Repo | Purpose |
|---|---|
| [synaptic-fx-terminal](https://github.com/Synaptics-Lab/synaptic-fx-terminal) | Institutional FX terminal and settlement engine (BankerX) |
| [FDC3PaymentsAdaptor](https://github.com/Synaptics-Lab/FDC3PaymentsAdaptor) | Estate-owned FDC3 payments adaptor (FINOS-Labs incubation) |
| [finITe](https://github.com/Synaptics-Lab/finITe) | FINOS FDC3 conformance suite, pinned and re-runnable against our desktop agent (131/132 ×2 receipts included) |
| [traderX](https://github.com/Synaptics-Lab/traderX) | Upstream FINOS traderX fork — branch `feature/016-post-trade-settlement-bankerx` (PR #470 in review) |
| [FDC3](https://github.com/Synaptics-Lab/FDC3) | Upstream FINOS FDC3 fork — branch `feature/iso20022-payment-intent` (PR #2204 MERGED into finos/FDC3:main) |
| [open-eago](https://github.com/Synaptics-Lab/open-eago) | FINOS OpenEAGO engagement (PR #65) |
| [IBM_BOB_finos_connector](https://github.com/Synaptics-Lab/IBM_BOB_finos_connector) | IBM BOB ↔ FINOS connector work |
| [syn-stripe-bridge](https://github.com/Synaptics-Lab/syn-stripe-bridge) | Stripe-compatible honest card-rail shim — Stripe-shaped API over Solana devnet OUSD, honest-core refusals, readback-gated settlement (TD-019 Sovereign Stripe) |

**Protocol and tooling**

| Repo | Purpose |
|---|---|
| [synaptic-open](https://github.com/Synaptics-Lab/synaptic-open) | Run SynapticChain L1 without the proprietary source: production node binaries + genesis, example SynapticLang contracts, live receipts, runnable probes (local node 3/3 ×2, public surface 7/7 ×2) |
| [x402-tswp](https://github.com/Synaptics-Lab/x402-tswp) | X402-TSWP SSOT — IETF draft `draft-shabazz-http-x402-tswp-00`, IANA-registered ALPN, and the 20-subsystem technical-disclosure registry (Zenodo DOIs) |
| [elizaos-plugin-x402-settlement](https://github.com/Synaptics-Lab/elizaos-plugin-x402-settlement) | Settlement plugin published to npm for the ElizaOS agent ecosystem |
| [synlang](https://github.com/Synaptics-Lab/synlang) | SynapticLang compiler CLI |
| [quantumshield-sovereign-dpi](https://github.com/Synaptics-Lab/quantumshield-sovereign-dpi) | 5-rail post-quantum shield (CE-WOTS+) |

The remaining repos in this organization are upstream open-source projects
pinned here for our contribution work (FINOS FDC3/traderX, modelcontextprotocol,
agent frameworks, quant libraries). Their content is upstream's; our changes live
in the branches named above and in the estate repositories.

---

## Upstream engagement

- **FINOS FDC3 #2204** — merged into finos/FDC3:main (2026-10-08, API-verified)
- **Solana SID proposal** — "Typed Settlement Wire Linkage via SPL Memo v2 and Token-2022 Introspection" — merged into our `solana-improvement-documents:main` as that repo's first-ever PR (#1, 2026-09-26)
- **FINOS traderX #470** — open, in active maintainer review
- **FINOS OpenEAGO #65** — open
- **finITe** — conformance suite pinned and re-runnable against our agent, receipts included

## Live estate

- **Explorer** — [explorer.synapticchain.xyz](https://explorer.synapticchain.xyz)
- **Wallet** — [wallet.synapticchain.xyz](https://wallet.synapticchain.xyz)
- **Landing** — [synapticchain.xyz](https://synapticchain.xyz)
- Testnet rails named exactly, always: **XRPL TESTNET (altnet)**, **Solana DEVNET**, **SynapticChain L1 testnet**.

---

## Contact

For partnership inquiries, investor relations, or technical questions, open an
issue on the relevant repository.

*SynapticChain — Rewiring value transfer.*