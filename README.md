# Tony Jagodka

I build **identity and payment infrastructure for the agentic web** — end-to-end and solo, under [UIG Studios LLC](https://uigstudios.netlify.app). Most of it ships on **Sui**.

> **The throughline:** x402 proves an agent *paid* · my settlement-receipt binding proves the payment maps to the *action* · **PoR** proves the actor is a *real, human-backed* entity. Together that's a **verified agent** — and I've shipped a working piece of every layer.

*Right now: **x402-sui-stack** and **FairLine** in **Sui Overflow 2026**, and co-authoring an **x402 standard extension** with [@vaaraio](https://github.com/vaaraio).*

---

### 🪪 Proof of Real (PoR) — flagship
A Sui-native proof-of-personhood credential: prove you're a real, unique human (passkey + zkLogin onboarding, no personal data captured) and raise your assurance through verifiable real-world actions.
- Live credential, attestor & Move package · SDK on npm → [`por-sdk`](https://www.npmjs.com/package/por-sdk) (Apache-2.0)
- Live in production today, Sybil-gating real users in a shipped app
- **[por-proof-of-real.netlify.app](https://por-proof-of-real.netlify.app)** · *mainnet contracts, testnet attestor — personhood, not "sybil-proof"*

### ⚡ x402 on Sui — the payments layer
- **[x402-sui-stack](https://x402-sui-stack.netlify.app)** — the x402 builder stack for Sui (**Sui Overflow 2026**): the facilitator + tooling + a one-command demo that settles a real $0.01 USDC payment on **mainnet** and lets anyone recompute it in-browser → [live](https://x402-sui-stack.netlify.app) · [code](https://github.com/DrVelvetFog/x402-sui-stack)
- **x402 facilitator that settles on Sui** — non-custodial, zero-fee, live on **mainnet** → [sui-x402-facilitator](https://github.com/DrVelvetFog/sui-x402-facilitator) · [live facilitator](https://sui-facilitator.onrender.com)
- **Co-authoring an x402 standard extension** — *Settlement-Receipt Binding*: bind an on-chain settlement to a signed execution receipt, recomputable from published bytes with an independent verifier → [x402-foundation/x402#2666](https://github.com/x402-foundation/x402/pull/2666)
- **[x402-pilot](https://github.com/DrVelvetFog/x402-pilot)** — an open-source, non-custodial x402 dev tool + conformance MCP (Apache-2.0)

### 🌊 FairLine — Sui Overflow 2026, DeepBook track
A risk-managed, multi-user liquidity vault on **DeepBook Predict** — "be the house, verifiably": senior/junior tranches, capacity cap, on-chain reserve floor + emergency pause, redemption-anchored NAV.
- **[fairline-vault.netlify.app](https://fairline-vault.netlify.app)** · *testnet, unaudited*

---

### Also shipped
- **[Acre](https://acre-game.netlify.app)** — a "walk your city" Sui game with gasless onboarding, **Sybil-gated by PoR** (live testnet)
- **[Gulp City](https://gulp-city.netlify.app)** — an installable 3D PWA arcade game
- **[Jamie Buddy](https://uigstudios.gumroad.com/l/jamie)** — a local-LLM writing assistant
- **Yomp** — an on-chain move-to-earn fitness app (Sui testnet) that feeds PoR's real-world-action layer

---

### Work with me
Open to **grants, contract & consulting** on Sui — identity, x402 / agentic payments, and shipped on-chain product.

📫 **tjagodka@gmail.com** · 🌐 [portfolio](https://tony-jagodka.netlify.app) · 🏢 [UIG Studios](https://uigstudios.netlify.app)

*Lines I don't cross: no custody · no token-for-money sales · no PII capture · honest labeling (testnet/unaudited stated plainly).*
