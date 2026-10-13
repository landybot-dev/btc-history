# btc-history

Public BTC/USD candle history snapshots for the BTC paper trader.

This repository holds **data only**: no code, no credentials. Snapshots are published as
versioned GitHub releases tagged `history-YYYYMMDD[-N]`. Each release contains:

- `history.tar.gz.part-*`: the exported history store, split into parts under 100 MB each
- `manifest.json`: each part's name, size and SHA-256, the SHA-256 of the whole archive,
  the earliest/latest candle and count for every timeframe (1m, 5m, 15m, 1h, 4h, 12h, 1d, 1w),
  and the snapshot's `through` time

The paper trader downloads the latest release on first launch without a token, checks every
checksum, and imports it only if all checks pass. A nightly job publishes a new snapshot with
newly closed candles and keeps the newest 7 releases.

Candles contain closed bars only. Each candle records its source exchange and build method.
Gaps are left marked as gaps and are never interpolated.

## Data sources and license note

Candles are built from the public market-data APIs of the source exchanges (primarily
Bitstamp BTC/USD, with Bitfinex as a fallback). The exchanges own the underlying market data
and their terms of service apply. This compilation is provided as is, without warranty, for
paper trading, research and education only. It is not financial advice and is not an official
exchange product. Do not use it for real trading decisions.
