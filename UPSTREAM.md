# Upstream — the full ledger

Every contribution I've made to code I don't own: merged, open, declined, and under embargo. Statuses are
current as of **2026-09-24** and each one links to the thread, so anything here can be checked rather than
taken on my word.

Eleven problem domains — HTTP framing, DNS zone files, DICOM medical imaging, medical NLP, RSS parsing,
supply-chain signing, SBOM formats, container image builds, package metadata, an L1 bridge, and a local-AI
IDE — across **Python, Rust, Go, TypeScript and Solidity**.

---

## Merged — 20 pull requests, 8 organisations

| Project | Domain | Lang | What |
|---|---|---|---|
| [openmed](https://github.com/maziyarpanahi/openmed) ×10 | medical NLP | Python | Release provenance end to end: a run-ledger binding every artifact to the gate decision that cleared it, the rollback decision that consumes it, Sigstore release signing, a catalog-coherence CI gate, a model-registry rekey, a multimodal preflight pair, and a decoded-memory planner for multimodal batches. Shipped as the headline feature of **OpenMed 2.1.0**, whose release notes thank me by name. |
| [huggingface.js](https://github.com/huggingface/huggingface.js) ×2 | ML tooling | TypeScript | `language()` used `code in TABLE`, and `in` walks the prototype chain — so `language("toString")` returned a *function* out of a signature typed `Language \| null`. Separately, a completed SHA-256 hash left its abort listener attached, so a later abort killed a worker already returned to the pool. |
| [sigstore-python](https://github.com/sigstore/sigstore-python) | supply-chain signing | Python | `Statement(contents=…)` swallowed the pydantic `ValidationError`, so three different failures all surfaced as one bare `malformed in-toto statement` with no `__cause__`. |
| [syft](https://github.com/anchore/syft) ×2 | SBOM formats | Go | A *valid* SPDX 2.3 document crashed both syft and grype, Anchore's vulnerability scanner. When the package the document describes is a file with no supplier (an optional field), `fileSource` dereferenced the nil supplier that `containerSource`, right above it, already checked. The same fix drops JSON `null` list entries that panicked elsewhere in the same decoder. The first crash came from a native Go fuzz target on `format.Decode`, about five minutes in, answering a 2022 maintainer request for fuzzing ([grype#981](https://github.com/anchore/grype/issues/981)). A round-trip target then caught syft writing SPDX it couldn't read back: with no source name, the root package got an empty `PackageName`, which SPDX requires, and tag-value output dropped the line entirely. |
| [agent-evidence-vocabulary](https://github.com/probityai/agent-evidence-vocabulary) ×2 | agent evidence | YAML / JSON | A crosswalk filing the aee-e2 verifier against a closed vocabulary for agent-evidence claims, plus the refusal-code mapping requested on [in-toto/attestation#570](https://github.com/in-toto/attestation/issues/570): 63 codes on each side, zero verbatim overlap, and 28 pairs that refuse exactly the same statements across the 209 reject vectors. A follow-up moved aee-e2's result row from *inferred* to *recomputed*, after recounting all 61 accepted rows from the raw first run rather than copying the total. |
| [x402](https://github.com/x402-foundation/x402) | payments standard | TypeScript | Cross-SDK `exact` error-code parity — the TS SDK was the lone outlier against Go and Python. Now sits in a Linux Foundation project. |
| [Nodle rollup](https://github.com/NodleCode/rollup) | L1 bridge | Solidity | Migrated the bridge's deposit and quote paths off the deprecated ZKsync Mailbox to Bridgehub. Commits landed with authorship preserved after the maintainer validated them against forked mainnet state. |
| [Tessera](https://github.com/neuratile/Tessera) | local-AI IDE | Rust | A `recovery_hint()` API across the error types. |

## Credited in the maintainer's own fix

Four bugs from one fuzzing run of NLnet Labs' Rust DNS library, reported privately and fixed in
**domain 0.12.3** (25 Sep 2026). The release notes and the RustSec advisory,
[RUSTSEC-2026-0310](https://rustsec.org/advisories/RUSTSEC-2026-0310.html), credit me by name alongside
the other reporters, including an independent report from Qifan Zhang of Palo Alto Networks.

| Project | Lang | What |
|---|---|---|
| [NLnetLabs/domain#730](https://github.com/NLnetLabs/domain/pull/730) | Rust | **Soundness.** The zone-file scanner's UTF-8 decoder accepted overlong encodings, then built a `&str` with `from_utf8_unchecked`, so a safe API could hand back a string that isn't valid UTF-8. That's undefined behaviour, and a bypass for any code that validates by characters. The same root cause let an overlong `;` trip an internal assertion. |
| [NLnetLabs/domain#736](https://github.com/NLnetLabs/domain/pull/736) | Rust | Any TXT record with no data, like `a. 300 IN TXT`, panicked with an index out of bounds. |
| [NLnetLabs/domain#725](https://github.com/NLnetLabs/domain/pull/725) | Rust | An integer overflow in the zone-file `Scan` implementation for unsigned integers: `checked_mul` guarded the multiply but `+=` was unchecked, so a release build silently wrapped. `MX 65536` parsed as preference `0`. |

## Open — under review

| Project | Domain | Lang | What | Status |
|---|---|---|---|---|
| [cpython#157952](https://github.com/python/cpython/pull/157952) | HTTP stdlib | Python | `http.client` hung forever reading a 204 or 304 that carried `Transfer-Encoding: chunked`. `begin()` set `length=0` for bodiless statuses but left `self.chunked=True`, and `read()` only guarded HEAD — so no timeout, no error, just a stall. Inherited by urllib3 and requests. RFC 9112 §6.1 explicitly permits that response. ([issue #157951](https://github.com/python/cpython/issues/157951)) | **approved**, awaiting a core dev |
| [apko#2523](https://github.com/chainguard-dev/apko/pull/2523) | container image builds | Go | apko had no fuzz targets. Added two for the APKINDEX parser, and the round-trip one failed in 65 seconds: `bufio.ScanLines` strips exactly one trailing `\r`, so a package named `0\r` is written back as `0`. That's a name change on the seam where melange writes indexes and apko reads them back. ([issue #2522](https://github.com/chainguard-dev/apko/issues/2522)) | open |
| [attohttpc#202](https://github.com/sbstp/attohttpc/pull/202) | HTTP client | Rust | `BodyReader::new` ignored both status and method, so HEAD responses with `Content-Length` — nearly all of them — plus every 204 and 304 hung until the timeout. 3.0s → 2ms after the fix. ([issue #201](https://github.com/sbstp/attohttpc/issues/201)) | open |
| [pydicom#2372](https://github.com/pydicom/pydicom/pull/2372) | medical imaging | Python | Encapsulated Pixel Data with fewer frames than `NumberOfFrames` raised a bare `StopIteration` — which inside `map()` **silently truncates**, dropping the malformed scan *and every good one after it*. They already warned on excess frames; missing frames were never handled. ([issue #2371](https://github.com/pydicom/pydicom/issues/2371)) | review requested |
| [purldb#907](https://github.com/aboutcode-org/purldb/issues/907) | package metadata | Python | Proposal: collect publisher provenance attestations for PyPI and npm packages. | open |
| [feedparser#599](https://github.com/kurtmckee/feedparser/issues/599) | RSS parsing | Python | `parse()` is contracted never to raise — it sets `bozo` instead. Fuzzing found ~12 root-cause families that escape it on the released version. Three fixed, ten more minimized and tabled in the issue. | open |

## Declined — and why

Worth listing, because a ledger that only shows wins isn't a ledger.

- **[feedparser#600](https://github.com/kurtmckee/feedparser/pull/600)** — closed by the maintainer as
  AI-generated. The three bugs it fixed are real and reproduce on the released version; they're still
  documented in issue #599 for whoever wants them.
- **[ersilia#1923](https://github.com/ersilia-os/ersilia/pull/1923)** — `ersilia close` left the served model
  process running. Closed because their team already had a fix in flight.

## Under coordinated disclosure

Details withheld until the maintainers ship. Listed so the record is complete, not to claim credit early.

- **actix-web / actix-http** — a response-desync issue in the client decoder. Private advisory filed via
  GitHub's vulnerability reporting, currently in triage. Reproduction and patch supplied.

---

## The method

No mystery to it, and it's repeatable:

1. **Screen for the gap.** Rank a language's most-depended-on parser, encoding, network and crypto packages
   by downloads, then drop everything already in OSS-Fuzz. Of 349 popular Rust crates, 246 had no fuzz
   target. The same screen over 42 supply-chain security repos found 34 with no fuzz target in the repo,
   grype and syft among them, though grype's maintainers had asked for one in 2022. ⚠️ "No `fuzz/` directory" is *not* the same as unfuzzed — several are fuzzed downstream by a
   consumer. Check for that before spending an evening.
2. **Fuzz the *published* version,** not just `main`. A bug that only exists on a development branch isn't
   affecting anyone yet.
3. **Triage against the contract.** Most crashes are worthless — a panic from misusing an API isn't a bug.
   The valuable ones violate something the project actually promises, or an RFC it claims to implement.
4. **Generalize the class.** The CPython, attohttpc and actix findings are one bug — *bodiless HTTP statuses
   whose framing headers are still honored* — found by taking a single actix discovery and sweeping eleven
   HTTP clients across four languages with one raw-socket server. Five were correct. Three were not.
5. **Ship the smallest fix with a regression test that fails without it,** plus the project's own changelog
   format. Then report it the way that project's `SECURITY.md` asks, which sometimes means telling nobody
   publicly for a while.

Findings are agent-assisted and I say so on the thread when a project asks. The reproduction, the fix and the
test are the part that matters, and those either hold up or they don't.

**→ [back to the profile](README.md)** · [the long-form portfolio](PORTFOLIO.md)
