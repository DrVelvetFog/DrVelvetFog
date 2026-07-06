# Tony Jagodka

I build **identity and payment infrastructure for the agentic web** — end-to-end and solo, under [UIG Studios LLC](https://uigstudios.netlify.app). Shipped deepest on **Sui**, taking the same settlement-semantics work cross-rail to **Solana / SVM** and **EVM**.

> **The throughline:** x402 proves an agent *paid* · my settlement-receipt binding proves the payment maps to the *action* · **PoR** proves the actor is a *real, human-backed* entity. Together that's a **verified agent** — and I've shipped a working piece of every layer.

*Right now: my **x402 Settlement-Receipt Binding** extension is [ready-for-review](https://github.com/x402-foundation/x402/pull/2666), its conformance gate reproduced green by independent issuers across two rails — and I'm taking the same settlement-semantics work cross-rail to **Solana / SVM**, now running end-to-end in an [x402 charging agent](https://github.com/DrVelvetFog/x402-charging-agent) (an EV that pays for its own charge — mainnet on Sui, settling on Solana devnet).*

---

### 🪪 Proof of Real (PoR) — flagship
A Sui-native proof-of-personhood credential: prove you're a real, unique human (passkey + zkLogin onboarding, no personal data captured) and raise your assurance through verifiable real-world actions.
- Live credential, attestor & Move package · SDK on npm → [`por-sdk`](https://www.npmjs.com/package/por-sdk) (Apache-2.0)
- **Device-attested real-world action** — App Attest proven on a real iPhone: a walk mints an on-chain *Verified Real* credential, end-to-end (one credential per attested device)
- Sybil-gating a live integration (Acre) — the credential gate runs in a shipped app, on-chain
- **[por-proof-of-real.netlify.app](https://por-proof-of-real.netlify.app)** · *mainnet contracts, testnet attestor — personhood, not "sybil-proof"*

### ⚡ x402 / agent payments — the payments layer
- **[x402-sui-stack](https://x402-sui-stack.netlify.app)** — the x402 builder stack for Sui (**Sui Overflow 2026**): the facilitator + tooling + a one-command demo that settles a real $0.01 USDC payment on **mainnet** and lets anyone recompute it in-browser → [live](https://x402-sui-stack.netlify.app) · [code](https://github.com/DrVelvetFog/x402-sui-stack)
- **x402 facilitator that settles on Sui** — non-custodial, zero-fee, live on **mainnet** → [sui-x402-facilitator](https://github.com/DrVelvetFog/sui-x402-facilitator) · [live facilitator](https://sui-facilitator.onrender.com)
- **Authoring a proposed x402 standard extension** — *Settlement-Receipt Binding*: bind an on-chain settlement to a signed execution receipt, recomputable from published bytes with an independent verifier — its conformance gate reproduced green by two independent issuers across two rails, plus a live gasless-Sui settlement vector → [x402-foundation/x402#2666](https://github.com/x402-foundation/x402/pull/2666)
- **Taking the standard cross-rail** — a [conformance demo for Solana's `upto` scheme](https://github.com/solana-foundation/x402/pull/3) proving settlement-receipt binding on SVM, plus shaping the `verify()`-soundness invariant on Hedera ([#2701](https://github.com/x402-foundation/x402/issues/2701)) and Solana's allowance-draw design ([#2699](https://github.com/x402-foundation/x402/issues/2699)); one binding, multiple rails (EVM · SVM · Sui)
- **[x402-pilot](https://github.com/DrVelvetFog/x402-pilot)** — an open-source, non-custodial x402 dev tool + conformance MCP (Apache-2.0)

### 🔌 x402 Charging Agent — the thesis, end-to-end
An EV that pays for its own charge, no human in the loop — the whole stack composed in one artifact:
- **x402 `upto`** metered billing + my **Settlement-Receipt Binding** (#2666) over a *real-world action* — authorize a ceiling, meter the kWh, settle the actual, emit a receipt an independent checker verifies
- **PoR-gated** — only a verified human's agent may charge (the personhood layer, live)
- **mainnet-proven on Sui**, also settling on **Solana devnet**; bridged to real charging networks via **OCPI** (DeCharge / Starpower-ready)
- **[x402-charging-agent](https://github.com/DrVelvetFog/x402-charging-agent)** · *vehicle + charging network mocked behind their real interfaces*

### 🌊 FairLine — Sui Overflow 2026, DeepBook track
A risk-managed, multi-user liquidity vault on **DeepBook Predict** — "be the house, verifiably": senior/junior tranches, capacity cap, on-chain reserve floor + emergency pause, redemption-anchored NAV.
- **[fairline-vault.netlify.app](https://fairline-vault.netlify.app)** · *testnet, unaudited*

---

### Also shipped
- **[Acre](https://acre-game.netlify.app)** — a "walk your city" Sui game with gasless onboarding, **Sybil-gated by PoR** (live testnet)
- **[Gulp City](https://gulp-city.netlify.app)** — an installable 3D PWA arcade game
- **[Jamie Buddy](https://uigstudios.gumroad.com/l/jamie)** — a local-LLM writing assistant
- **Yomp** — the consumer front door for PoR: *walk to prove you're real* (Sui testnet). The walk is what mints the credential's real-world-action tier.

---

### Upstream contributions
Code merged into repos I don't maintain:
- **[openmed](https://github.com/maziyarpanahi/openmed)** (medical NLP · 4.2k★) — an interactive synthetic-data Gradio de-identification demo, and a memory-mapping toggle for the MLX weight-loading path, both with import-safe test coverage → [#1023](https://github.com/maziyarpanahi/openmed/pull/1023) · [#1024](https://github.com/maziyarpanahi/openmed/pull/1024)
- **[Tessera](https://github.com/neuratile/Tessera)** — a `recovery_hint()` API across the error types of a local-first AI testing IDE (Rust) → [#103](https://github.com/neuratile/Tessera/pull/103)
- **[x402](https://github.com/x402-foundation/x402)** — a cross-SDK `exact` error-code parity fix (the TS SDK was the lone outlier vs Go / Python) → [#2744](https://github.com/x402-foundation/x402/pull/2744)
- **[Nodle rollup](https://github.com/NodleCode/rollup)** — docs for manual on-chain vested-grant claims → [#120](https://github.com/NodleCode/rollup/pull/120)

Contributing upstream to **Mysten's Sui stack** — filed a cached-price payment race in `@mysten/walrus` that was taking out mainnet writes ([ts-sdks#1127](https://github.com/MystenLabs/ts-sdks/issues/1127)), reviewed the maintainer's fix ([#1128](https://github.com/MystenLabs/ts-sdks/pull/1128)), and reviewed the [MemWal relayer's recovery](https://github.com/MystenLabs/MemWal/pull/352) for the same class of bug.

---

### Work with me
**Available for contract, consulting, grants & engineering roles** — identity and x402 / agentic payments, **across Sui, Solana/SVM and EVM**. Deepest on Sui, actively building cross-rail.

📫 **tjagodka@gmail.com** · 𝕏 [@DrVelvetFog](https://x.com/DrVelvetFog) · 🌐 [portfolio](https://tony-jagodka.netlify.app) · 💼 [Algora](https://algora.io/DrVelvetFog) · 🏢 [UIG Studios](https://uigstudios.netlify.app)

*Lines I don't cross: no custody · no token-for-money sales · no PII capture · honest labeling (testnet/unaudited stated plainly).*
