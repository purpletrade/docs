# purple.trade

**Synthetic leverage trading for any token on Solana.**

purple.trade is the first platform that turns any token into a perpetual futures market — fully on-chain, no off-chain orderbook, no sequencer, no bridge. Powered by the [Percolator engine](https://github.com/purpletrade/percolator-prog), an open-source perpetual futures protocol created by Solana co-founder [Anatoly Yakovenko](https://x.com/toly).

## How it works

Every market is an **inverted perpetual** — the token itself is the collateral. No stablecoins, no wrapped assets, no borrowing. One Solana account (a "slab") holds the entire market state: positions, collateral, funding, insurance fund. Every trade settles atomically in a single transaction.

```
User wallet  →  [KeeperCrank + TradeCpi]  →  Slab account  ←  vAMM matcher (CPI)
                                                   ↑
                                              Oracle price
```

**Launch pipeline:** Token creation → Meteora bonding curve → bond threshold → auto-deploy Percolator market. From idea to leveraged trading in minutes.

## Trading parameters

| | |
|---|---|
| Leverage | Up to 10x |
| Initial margin | 10% |
| Maintenance margin | 5% |
| Trading fee | 0.1% |
| Collateral | The token itself |

## Protocol

Four open-source repositories make up the Percolator protocol:

| Repository | Description |
|---|---|
| [percolator-prog](https://github.com/purpletrade/percolator-prog) | Core perpetual futures engine (Rust, ~4,400 lines) |
| [percolator-match](https://github.com/purpletrade/percolator-match) | Passive LP matcher — vAMM pricing via CPI |
| [percolator-cli](https://github.com/purpletrade/percolator-cli) | CLI and operational tooling |
| [percolator](https://github.com/purpletrade/percolator) | Formally verified risk engine (143 Kani proofs) |

Programs are deployed with **verified builds**, **OtterSec verification**, and embedded **security.txt**. The TypeScript SDK is audited byte-for-byte against the Rust source. See the [verification docs](https://purple.trade/docs/verification) for SHA-256 hashes and reproduction instructions.

## Programs

| Network | Program | Address |
|---|---|---|
| Mainnet | Matcher | [`MTCPqs6RWWUPMHhvZnnB6BLAXS86TDpTaxQW7Pa3aDh`](https://solscan.io/account/MTCPqs6RWWUPMHhvZnnB6BLAXS86TDpTaxQW7Pa3aDh) |
| Mainnet | Percolator | [`PRPLUgjCUxCEzNPP6x7XJVK1WR5XX28Zu8MEyTqvGjF`](https://solscan.io/account/PRPLUgjCUxCEzNPP6x7XJVK1WR5XX28Zu8MEyTqvGjF) |
| Devnet | Percolator | `2SSnp35m7FQ7cRLNKGdW5UzjYFF6RBUNq7d3m5mqNByp` |
| Devnet | Matcher | `4HcGCsyjAqnFua5ccuXyt8KRRQzKFbGTJkVChpS7Yfzy` |

## Documentation

This repo powers the docs at [purple.trade/docs](https://purple.trade/docs), built with [Mintlify](https://mintlify.com).

```
docs.json            Mintlify config, navigation, theme
index.mdx            Landing — what is purple.trade
trading.mdx          Trading guide — margins, fees, inverted perps
launch.mdx           Token launch pipeline — Meteora DBC → auto-deploy
percolator.mdx       Percolator engine deep-dive — slabs, instructions, oracle, risk
history.mdx          Origins — Toly's creation, SOV model, fork story
verification.mdx     Don't trust, verify — SBF builds, SDK audit, Kani proofs
programs.mdx         Program IDs and deployment addresses
repo-*.mdx           Per-repository documentation
```

### Local development

```bash
npm i -g mint
mint dev
# http://localhost:3000
```

### Links

- [purple.trade](https://purple.trade)
- [Documentation](https://purple.trade/docs)
- [Twitter](https://x.com/tradeonpurple)
- [GitHub](https://github.com/purpletrade)
