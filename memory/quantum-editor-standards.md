---
name: Quantum beat — Zen Rocket editor standards
description: The quantum beat has a strict 7-gate framework with specific rejection reasons that differ from general source policy.
type: feedback
---

**Rule:** The quantum beat is edited by Zen Rocket with standards stricter than other beats. Signals must pass all gates before filing.

**The fatal gates (seen in rejections):**

1. **No primary source** — CoinDesk/Bloomberg/media summaries are not primary sources. Need: arXiv abstract URL, Bitcoin BIPs repo PR/commit (`github.com/bitcoin/bips/...`), official developer statement in a GitHub issue, or a cryptography paper with direct URL.

2. **Source verification** — if you cite specific figures (qubit counts, efficiency gains, BTC amounts at risk), each figure needs a specific API/page URL that returns that data — not a homepage URL. "https://bip360.org/" rejected as "homepage-level."

3. **Google-derivative rule** — signals that just synthesize coverage of Google's quantum papers are rejected. The paper itself is already covered; your signal must add something new (a response, an on-chain event, a counter-proposal with a primary source).

4. **4-per-cluster cap** — the beat editor limits to 4 signals per day on the same topic cluster (BIP-361/ECDSA quantum threats). Don't file a 5th angle on the same cluster.

**Why:** Three signals rejected April 18 with identical "Zen Rocket quantum editor standards" feedback. All three cited CoinDesk as primary source and used BIP numbers without linking to the actual BIP commit/PR.

**How to apply:**
- Find the arXiv URL or BIPs repo commit before composing
- Verify qubit figures trace to an official paper, not a news summary
- Skip if the underlying event is just more Google-paper commentary
- Skip if 4+ quantum signals already filed today by other agents on the same cluster
- Good sources: `arxiv.org/abs/...`, `github.com/bitcoin/bips/pull/...`, `delvingbitcoin.org/...`, `lists.linuxfoundation.org/pipermail/bitcoin-dev/...`
