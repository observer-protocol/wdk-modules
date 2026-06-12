# Observer Protocol — WDK modules

Native modules for the Tether [Wallet Development Kit](https://github.com/tetherto/wdk) ecosystem. Each module is published as its own `@observer-protocol/wdk-*` npm package; this repository is the index, not a monorepo.

## Available modules

### Policy enforcement
**[@observer-protocol/wdk-op-policy](https://github.com/observer-protocol/wdk-op-policy)** — `v0.1.0`

Delegation-scoped, pre-signature policy enforcement for agentic wallets, via the Tether WDK transaction policy engine ([PR #55](https://github.com/tetherto/wdk/pull/55)). Registers an **ALLOW + DENY** policy pair (the DENY companion is the mandatory fail-closed backbone) that verifies a proposed write op against the `tradingMandate` in a signed `ObserverDelegationCredential` (per [AIP v0.8](https://github.com/observer-protocol/aip/blob/main/aip-v0.8-draft-1.md)) before the key signs. Verified against the published `@tetherto/wdk@1.0.0-beta.11` (26 conformance cases). Its portable, signed `PolicyEvaluationCredential` audit surface — a third-party-verifiable decision record issued by the Observer Protocol evaluator, **live at the protocol level today** — is being integrated into this module (v0.1 records a local audit log).

[Repository](https://github.com/observer-protocol/wdk-op-policy) · [Documentation](https://github.com/observer-protocol/wdk-op-policy#readme) · [npm](https://www.npmjs.com/package/@observer-protocol/wdk-op-policy)

---

### Trust attestation
**[@observer-protocol/wdk-protocol-trust](https://github.com/observer-protocol/wdk-protocol-trust)** — `v0.1.0-beta.1`

Agent identity + bilateral trust handshake. Binds a WDK wallet account to a W3C `did:web` agent identity registered on Observer Protocol; ERC-8004 payment attestation is optional. Per [AIP v0.6](https://github.com/observer-protocol/aip).

[Repository](https://github.com/observer-protocol/wdk-protocol-trust) · [Documentation](https://github.com/observer-protocol/wdk-protocol-trust#readme) · [npm](https://www.npmjs.com/package/@observer-protocol/wdk-protocol-trust)

---

### Lightning verification
**[@observer-protocol/wdk-lightning-verifier](https://github.com/observer-protocol/wdk-lightning-verifier)** — `v0.1.0-beta.1`

Verifiable Lightning Network payment verification for KYA flows: preimage proofs, transaction visibility, reputation attribution. Wallet-agnostic.

[Repository](https://github.com/observer-protocol/wdk-lightning-verifier) · [Documentation](https://github.com/observer-protocol/wdk-lightning-verifier#readme) · [npm](https://www.npmjs.com/package/@observer-protocol/wdk-lightning-verifier)

---

## Why three repos and not one monorepo

The Tether WDK ecosystem itself is module-per-repo (`tetherto/wdk`, `tetherto/wdk-wallet-btc`, `tetherto/wdk-wallet-spark`, and many more per-rail modules). Each of our modules follows that convention so it slots cleanly into the WDK module pattern Tether integrators are already familiar with.

This repository is the discovery layer — a single place to find all current WDK modules with their statuses and links. It carries no code.

## Integration guide

Each module's README is self-contained. For the protocol that ties them together, see:

- [AIP v0.8 draft 1](https://github.com/observer-protocol/aip/blob/main/aip-v0.8-draft-1.md) — current spec; introduces `PolicyEvaluationCredential` and the trading-mandate extensions consumed by `wdk-op-policy`.
- [AIP v0.6 draft 1](https://github.com/observer-protocol/aip/blob/main/aip-v0.6-draft-1.md) — core protocol; the W3C VC / DID primitives consumed by all modules.

## License

All modules are licensed under Apache-2.0.

## Historical

- [`wdk-observer-protocol`](https://github.com/observer-protocol/wdk-observer-protocol) — original 2026-03 hackathon submission. Superseded by `wdk-op-policy` and `wdk-protocol-trust`; archived, retained for reference only.
- [`wdk-policy`](https://github.com/observer-protocol/wdk-policy) — pre-#55 policy module (local mandate evaluation + a signed-decision sidecar client). Superseded by [`wdk-op-policy`](https://github.com/observer-protocol/wdk-op-policy), which enforces through Tether's merged WDK policy engine (PR #55). Archived; retained for reference — its `PolicyEvaluationCredential` sidecar client is the reference implementation for that roadmap surface.
