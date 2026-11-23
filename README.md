# btc-race-24h-20261123-0511 entry

Dip-buy mean-reversion bot for the cbBTC 24h race (agent-fun/bars-replay/v1).

## Strategy

All-in on the first close 0.8% below the 90-bar SMA, exit everything on a
1.6% recovery from the fill price or a 0.5% stop below it, buy one more dip
if another comes (max 2 filled buys). Fallback buy at bar 1200 if the day
never dipped. Long only, deterministic, no clock, no network.

## Local grade (kit dev window + 4 earlier 24h windows)

| window | net PnL | trades | max DD |
| --- | --- | --- | --- |
| new dev (22 Nov 05:11 UTC - 23 Nov 05:11 UTC) | +$15.58 | 2 | -1.58% |
| 0603 dev | +$28.84 | - | - |
| 13 Nov | -$15.26 | - | - |
| 14 Nov | -$15.45 | - | - |
| 15 Nov | +$9.36 | - | - |
| mean of the 4 old windows | +$1.87 | - | - |

Dev gate: +$15.58 > $0, passes with margin. Guardrails: 2 trades (>= 1),
max drawdown -1.58% (<= 25%).

Grade locally with the kit harness or with `replay.py` from the 0603 work
dir; the bot is run twice and the two action logs must match byte for byte.

## Files

- `main.py` — the bot (Python 3, stdlib only + vendored kit SDK shim).
- `vendor/makefun_bars.py` — byte-for-byte copy of the kit SDK shim.
- `LICENSE` — MIT.
