# Blitz T-DCA — public backtest artifacts

This repository holds the **result file** behind the backtest published at
<https://www.blitz-trading.com/backtest>, so that the SHA-256 printed on that
page can be checked by anyone.

It is a results archive, not a trading system. The engine source is not here.

## What is in this release

| File | Bytes | SHA-256 |
| --- | ---: | --- |
| `btc-futures-s14-40-n18-u75-20260824-public.report.json` | 12,240 | `1c3306db60746d534e4466ff590cc4fa03938d90f951906a84f7d3a62c122a0a` |

The hash above is the value printed on the website as **Report JSON SHA256**.
The file is byte-identical to the one the site links to.

The website also prints two more hashes for the same snapshot — **State SHA256**
(engine end-state) and **Excel SHA256** (a spreadsheet rendering). Those files
are **not** included in this release.

## Snapshot identity

| | |
| --- | --- |
| Public snapshot ID | `btc-futures-s14-40-n18-u75-20260824-public` |
| Instrument | BTCUSDT perpetual futures |
| Strategy key | s1-4 +40% · N18 · U75 · 5x · Cross · TP ROI 1.5% |
| Input data | Binance BTCUSDT aggTrades (trade-by-trade), 2021-01-01 → 2026-08-24 |
| Engine source commit | `8cff0b0500550cbc3d310eb9e63c17d7af74a714` |
| Report generated | 2026-08-25 |

The strategy parameters are the ones published on the site: an 18-step entry
ladder (N18) with steps 1–4 covering +40% of the ladder's range, 75% wallet
usage (U75), 5× leverage, cross margin, and take-profit at +1.5% margin ROI
(a +0.30% price move at 5×).

## How to verify

```
# Linux / macOS
sha256sum btc-futures-s14-40-n18-u75-20260824-public.report.json

# Windows (PowerShell)
Get-FileHash .\btc-futures-s14-40-n18-u75-20260824-public.report.json -Algorithm SHA256
```

Compare the output with the hash in the table above and with the **Report JSON
SHA256** line on <https://www.blitz-trading.com/backtest>. If any of the three
differ, the file has been altered.

## Headline figures in the file

These are the values the website reports. They are reproduced here only so a
reader can confirm the file and the site agree; the file is the source.

| Field | Value |
| --- | ---: |
| Starting wallet (USDT) | 133,333 |
| `final_wallet` | 2,201,183.98 |
| `profit` | 2,067,850.98 |
| `roi_pct` | +1,550.89 |
| `tp_count` (take-profits filled) | 14,018 |
| `liq_count` (liquidations) | 0 |
| `rebal_count` (wallet-growth resets) | 29 |
| `max_step` (deepest ladder step reached) | 18 of 18 |
| `total_fee` (trading fees paid, USDT) | 629,345.95 |
| `total_volume` (USDT) | 899,065,645 |
| Maximum account drawdown | **−81.31%** (published on the site; not a field in this file) |

Trading fees are deducted from the reported result. Funding and slippage are
not separately published for this snapshot.

## Field glossary

| Key | Meaning |
| --- | --- |
| `final_wallet`, `profit`, `roi_pct` | End wallet, net profit, and ROI over the full period, in USDT and percent |
| `tp_count`, `cycles_count` | Number of take-profit fills; equal to the number of completed cycles |
| `liq_count` | Liquidations during the run |
| `rebal_count` | Times the ladder was re-sized after wallet growth (the run reinvests via a +10% wallet-growth reset; the live bot does not reinvest automatically) |
| `max_step` | Deepest ladder step the run ever reached |
| `total_fee`, `total_volume` | Trading fees paid and notional traded, in USDT |
| `monthly`, `yearly` | The same counters broken down by calendar month and year |
| `open_at_end` | Position state at the end of the run |

## What this is not

- **Not live returns.** This is a historical simulation on recorded trades.
  Historical paths cannot reproduce future liquidity, fills, funding, or
  slippage. Trading involves risk of loss.
- **Not out-of-sample.** The strict out-of-sample window has not been opened.
- **Not the engine.** The code that produced this file is not published. What
  is published is the result, its provenance, and its hash.
- **Not custom settings.** The result covers exactly the preset above.

The site's full methodology, limitations, yearly drawdown, per-cycle MAE,
capital utilization, ladder-depth distribution, and fee/funding variants are at
<https://www.blitz-trading.com/backtest>.

## License

The data in this repository is released under
[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/),
the same license declared in the site's `Dataset` structured data.

Blitz Technologies Ltd. · <https://www.blitz-trading.com>
