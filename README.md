# Niekie crypto casino data

Monthly measurements of crypto casinos, published by [Niekie](https://niekie.app), an independent safety index for online casinos. Every figure here is recomputable from public sources: blockchains for payouts, the casinos' own public bet feeds for play.

Licensed [CC BY-SA 4.0](LICENSE). Use it freely, credit "Niekie" with a link to https://niekie.app, and share adaptations under the same terms.

## What is in it

### `payouts/YYYY-MM.csv`: payouts counted on-chain

One row per crypto casino whose wallets we have identified.

| Column | Meaning |
| --- | --- |
| `transfers_out` | Every transfer we counted leaving the casino's wallets that month |
| `payout_share_pct` | Share of the casino's sampled outbound transfers that look like a player payout: to an address that is not a known casino wallet, worth $5 to $250,000 at that day's price |
| `payouts_est` | `transfers_out` times `payout_share_pct`. Estimated for October 2026; counted transfer by transfer from November 2026 |
| `payouts_per_day_est` | `payouts_est` over the days in the month |
| `typical_payout_usd` | Median of the sampled payouts |
| `licence` | The licence as the casino states it, and whether a regulator's register confirmed it |
| `score_YYYY_MM_DD` | The casino's Niekie safety score (0 to 100) on that date |

Write-up: [Crypto Casino Payouts, October 2026](https://niekie.app/blog/crypto-casino-payouts-october-2026)

### `feeds/YYYY-MM.json` and `.csv`: what casinos' public bet feeds show

For each casino that publishes a feed of settled bets: rounds broadcast, the share that lost, and the aggregate return. Each JSON file carries a SHA-256 `hash` of its figures, matching the hash printed on [the issue page](https://niekie.app/review), so a copy can be checked against the original.

### `scores/YYYY-MM.csv`: safety scores at the end of each month

Each casino's Niekie safety score (0 to 100) as sealed on the public ledger at the end of the month: the score, its grade, the five pillar scores behind it, the month's low and high, and how many times the score was resealed that month. `hash` is the full SHA-256 of the sealed ledger entry; look it up on [the public ledger](https://niekie.app/proof) to check the row.

`method_version` matters when comparing months. The scoring method has changed, and so have the pillar scales (the licence pillar was out of 30 under 2.0 and out of 15 under 2.1). Compare overall scores across versions with care, and pillars only within one version. July 2026 covers the first weeks of scoring and includes early runs, which is why some monthly lows are very low.

From November 2026 the payout files use the live export's columns (`payouts`, `payouts_estimated`, licence status and score on the day of export); October 2026 is frozen exactly as its report published it.

## What this cannot tell you

- **Approval speed.** The chain shows when a payout leaves, not when a player asked for it.
- **Whether any one player was paid.** A high count is consistent with paying players, not proof of any single withdrawal.
- **Every transfer.** On a casino's busiest days we read only part of its traffic, so counts are a floor.
- **A game's true RTP.** A casino chooses which rounds its feed shows. The feed figures measure what is broadcast, not what a game pays.

## Cite

> Niekie (2026). *Niekie crypto casino data* [Data set]. https://github.com/vvvvv2000/niekie-crypto-casino-data

New months are added automatically on the 2nd of each month (`.github/workflows/monthly.yml`); a month already published is never changed.

Questions, corrections or a custom cut: contact@niekie.app. Compiled by Maj Jan Krošl. Method: https://niekie.app/how-we-score
