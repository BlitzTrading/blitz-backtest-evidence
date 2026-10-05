# Out-of-sample window 2026-08-25 → 2026-09-30 (BTC and ETH public presets)

This folder holds the public evidence for the first out-of-sample (OOS)
run of the two public presets shown at <https://www.blitz-trading.com/backtest>
(BTC) and <https://www.blitz-trading.com/backtest/eth> (ETH).

The presets were run **unchanged** on the 37 days after the historical
backtest period (which ended 2026-08-24), each with a fresh 133,333 USDT
wallet. Nothing was tuned or re-selected.

## Files

| File | Bytes | SHA-256 | What it is |
| --- | ---: | --- | --- |
| `public-presets-oos-20260825-20260930.summary.json` | 10,120 | `686c6cec07950f35075a56d35f94810702c3230f28d22d1966f5873db9fd9153` | Public results summary. The website's out-of-sample section links to a byte-identical copy. |
| `started-receipt.json` | 630 | `7026412ed6b1acd0f2afccf00ae24bcfc2d11a8e5df73bce7cdbf294099a7885` | Receipt written when the run started. Printed on the website as **Start receipt**. |
| `completed-receipt.json` | 805 | `ba63db6641f862621abe5b41c53795ae1ee727f596a37db35d78db4168aebcbb` | Receipt written when the run finished. Contains the results-file hash. |
| `inputs-manifest.json` | 93,407 | `2ef0f8c3075d6e5a612142105515144eaa279b48c3b44a6a05741e0035057865` | Every market-data file used for the run: Binance download URL, Binance's own checksum, and the hash of the extracted CSV. |

The receipts are copied byte for byte, so they still contain the original
local file paths and process ID. They were renamed for this folder; their
original names were `public-presets-oos-20260825-20260930.json` and
`public-presets-oos-20260825-20260930.status.json`, respectively.

This archive was made before the out-of-sample section was published on the
website. Where this README says what the website prints or links to, it means
that section as released with these files; check it against the live pages.

### Files that are hashed but not published

| File | SHA-256 | Why it is not here |
| --- | --- | --- |
| Frozen execution plan (`freeze_manifest.json`) | `eb22322279c59c7d34457419c9b1cc520210bd7773ab8ea49183573ddd90dc3f` | Contains the presets' exact internal ladder values, which are not public. Printed on the website as **Frozen execution plan**. |
| Results (`oos_results.json`) | `767d62c507d63fb59062774016e8b68761a967c112ec75df46d52bfbcf4de2b9` | Contains internal fields outside the public summary. Printed on the website as **Results**. The numbers in the summary are taken or derived from this file and the frozen plan (for example the number of ladder rounds, and the ETH exit price rounded to the price tick). |

Publishing the hashes means that if either file is disclosed later, anyone can
check it is the file that existed when this archive was made. Both files cite
the DOI of the historical snapshot (10.5281/zenodo.22809597) as a seal
reference. That was a mistake: that archive holds the BTC historical report
and the rounded settings published on the site, not the presets' exact
internal ladder values or anything about the ETH preset. The frozen files keep the
original wording.

## Results

The headline metric was fixed before the run: **exit-net return**, baseline
cost variant, full window. Exit-net values any position still open at the end
of the window at the 2026-09-30 23:59 UTC 1-minute mark-price close, net of
the cost of closing it (the exit fee and, for BTC, entry fees not yet
charged). The figures below are rounded from the summary JSON; the file is the
source.

| | BTC, full window | ETH, full window | ETH, partial window |
| --- | ---: | ---: | ---: |
| Window | 08-25 → 09-30 | 08-25 → 09-30 | 09-02 → 09-30, fresh wallet |
| Exit-net return (baseline) | **+1.53%** | **+1.37%** | +1.23% |
| Account max drawdown | −2.27% | −1.05% | −1.04% |
| Take-profit cycles | 141 | 259 | 239 |
| Liquidations | 0 | 0 | 0 |
| Deepest round reached, including the open position | 10 of 18 | 6 of 12 | 6 of 12 |
| Position at window end | round 8 open, −2.39% vs average entry | round 3 open, −1.20% | round 3 open, −1.18% |
| + funding | +1.37% | +1.34% | +1.21% |
| + funding, 1bp slippage | +1.27% | +1.28% | +1.16% |
| + funding, 2bp slippage | +1.17% | +1.22% | +1.10% |

- **BTC closed cycles only: +2.24%.** A round-8 position opened on
  2026-09-23 was still open at the end. Valuing it at the final mark price,
  after exit costs, lowers the result by 0.71 percentage points to +1.53%. The
  lower figure is the headline.
- Valuation marks (2026-09-30 23:59 UTC 1-minute mark-price close): BTCUSDT
  83,583.2930942; ETHUSDT 2,684.73687597. The ETH engine rounds the exit price
  down to the 0.01 price tick (2,684.73).
- Baseline means no funding and no take-profit slippage. The ETH engine still
  applies 1bp slippage to each cycle's first market entry in every variant.
- Drawdown basis differs by engine: BTC is measured on executed trade prices,
  ETH on 1-minute mark-price closes. Both include the unrealized loss of open
  positions.
- Fees, funding and slippage totals per variant are in the summary JSON.
- No annualized figure is published. 37 days is too short for one.

## ETH prior-use disclosure

ETH data for 2026-08-25 → 2026-09-01 had already been used by other research
that was rejected before the public ETH preset was chosen. The preset's ladder
was selected on 2026-09-07 and its wallet usage (U82) was fixed on
2026-09-08, both using data through 2026-08-24; market data from 2026-09-02
onward already existed at that time but was not used.

One exception: earlier historical ETH evaluations valued a position still open
at the end with the 2026-08-25 00:00 UTC mark-price minute and, on the
indirect evidence of a reviewer we commissioned, also charged the funding payment
settled at that minute in the funding scenarios. Both were corrected on
2026-09-30 and are disclosed on the ETH page. The runs used to choose the
preset used the same evaluation code, so they may also have read that minute.

So, apart from that one minute, the two ETH windows are labelled:

- **Full window (08-25 → 09-30): not used in preset selection.**
- **Partial window (09-02 → 09-30): not used in any prior research.** It is
  rerun from a fresh wallet.

No BTC strategy evaluation had opened data on or after 2026-08-25 before this
run.

## Timeline

| Time (UTC) | Event | Evidence |
| --- | --- | --- |
| 2026-08-25 18:24 | BTC preset's historical results and the report file's hash published on the website (production deployment finished; 2026-08-26 03:24 KST). See note 1. | site |
| 2026-09-07 00:52 | ETH preset's ladder selected, using data through 2026-08-24 (see the exception above) | private git repository |
| 2026-09-08 01:55 | ETH preset's wallet usage (U82) fixed, using data through 2026-08-24 (see the exception above) | private git repository |
| 2026-09-08 10:36 | ETH preset's historical results and the report file's hash published on the website (production deployment finished; 19:36 KST). See note 1. | site |
| 2026-10-05 11:58:18 | Execution plan frozen and committed (`79bc6ea7b7dccfba1893454824e4e8a4dd8ba448`) | private git repository |
| 2026-10-05 11:58:29 | Run started | `started-receipt.json` |
| 2026-10-05 12:02:24 | Run finished | `completed-receipt.json` |
| 2026-10-05 15:58 | Summary, receipts and hashes archived | GitHub release `oos-20260825-20260930`; Zenodo DOI [10.5281/zenodo.23166756](https://doi.org/10.5281/zenodo.23166756) |

The freeze, run and results were recorded in a private git repository
(runner `7bf1c54363802e065b6ac6cd2de03cfb44776a82`, freeze
`79bc6ea7b7dccfba1893454824e4e8a4dd8ba448`, results
`4cd305dbadd7b6c103b202d05b90a52fed957dcd`). This is **not** an external
pre-registration: git commit times are set by the committer. This archive
records these files and hashes as of the archive date; it does not by itself
prove the order of events on 2026-10-05.

The BTC hash was published on the website during the first day of the window,
about 18 hours after it opened. The `hashPublicationDates` in the summary JSON
are calendar dates in Korea Standard Time (UTC+9): BTC 2026-08-26 KST is
2026-08-25 UTC.

Note 1. The report hash printed on each page has changed once since it was
first published. BTC: the first hash,
`372965dff93bd8046464923742a03e86ccbc0462512119a1561d54fd6726b1e3`, was of the
original report file, which the website did not offer for download. On
2026-09-17 the report file was first offered for download, without two
internal fields and with every published figure unchanged, and the printed
hash became
`1c3306db60746d534e4466ff590cc4fa03938d90f951906a84f7d3a62c122a0a` (archived
in this repository as `snapshot-20260824`). ETH: the first hash,
`89da2e23c3c2b13c17ef309ea85d058b3592ee0ae573cb54a558569b88a5c5fa`, became
`7a849fd3db4fa12213491540d2891ae0e107854e20a71214bda9640221e9c852` on
2026-09-30, when the valuation minute described above was corrected; the ETH
page lists both.

The backtest engines were not modified for this run (BTC
`_s14_u75_instrumented.py`; ETH `eth_perp_v2.py` through
`run_btc_tick_eval.py`). The two engines are each internally consistent but
model fees differently; see `disclosures` in the summary JSON.

## Input data

All inputs are public Binance USD-M futures data for 2026-08-25 → 2026-09-30:

- aggTrades, daily (BTCUSDT and ETHUSDT, 37 days each) — the trade-by-trade
  price path.
- 1-minute klines and 1-minute markPriceKlines (daily files for August, the
  monthly file for September).
- Funding rates from the REST API `fapi/v1/fundingRate` (111 rows per symbol).

`inputs-manifest.json` lists every file. On 2026-10-05 every aggTrades zip was
downloaded again: each zip matched Binance's `.CHECKSUM`, and each extracted
CSV matched, byte for byte, the local CSV prepared for the run. The BTC engine
read those CSVs directly; the ETH engine read tick files converted from them
before the freeze (the frozen plan records the converted files' hashes). The
kline and mark-price zips had been checked against `.CHECKSUM` when they were
first downloaded, and
their extracted CSVs and the funding files match the hashes in the frozen
plan. In all, 251 checks passed and none failed. To check one yourself:

```
# Linux / macOS
curl -O https://data.binance.vision/data/futures/um/daily/aggTrades/BTCUSDT/BTCUSDT-aggTrades-2026-09-12.zip
curl -O https://data.binance.vision/data/futures/um/daily/aggTrades/BTCUSDT/BTCUSDT-aggTrades-2026-09-12.zip.CHECKSUM
sha256sum -c BTCUSDT-aggTrades-2026-09-12.zip.CHECKSUM
unzip -p BTCUSDT-aggTrades-2026-09-12.zip | sha256sum
# compare with csv_sha256 for that date in inputs-manifest.json
```

## How to verify the summary

```
# Linux / macOS
sha256sum public-presets-oos-20260825-20260930.summary.json

# Windows (PowerShell)
Get-FileHash .\public-presets-oos-20260825-20260930.summary.json -Algorithm SHA256
```

Compare with the table above, with the file downloaded from
<https://www.blitz-trading.com/evidence/public-presets-oos-20260825-20260930.summary.json>
(once the out-of-sample section is live), and with the copy inside the Zenodo
archive. If any differ, a file has been
altered.

## What this is not

- **Not live returns.** It is a simulation on recorded market data. It cannot
  reproduce future liquidity, fills, funding or slippage. Trading involves risk
  of loss.
- **Not a long-run estimate.** 37 days is a short window. The full historical
  backtests reached max drawdowns of −81.31% (BTC) and −50.24% (ETH).
- **Not the engine.** The code is not published; the results, inputs and
  hashes are.

The next out-of-sample window is Q4 2026 (2026-10-01 → 2026-12-31), to be
published in early January 2027 with the same presets, unchanged, and an
execution plan frozen before the run, whatever the result.

## License

CC BY 4.0, as for the rest of this repository.

Blitz Technologies Ltd. · <https://www.blitz-trading.com>
