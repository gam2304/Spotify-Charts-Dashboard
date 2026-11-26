# Data

The raw Spotify chart CSV files are **not** stored in this repository, because of their size and redistribution terms.

## Source

- Dataset: _name, author and link_
- Licence: _licence / terms of use_
- Files used: nine yearly CSV files of weekly Spotify Top 200 chart positions (for example `spotify_top200_positions_2026.csv`).

## Expected columns (FactSpotify)

`week_end`, `CountryCode`, `rank`, `prev_rank`, `peak`, `appearances`, `entry_status`, `track_id`, `title`, `artists`, `artist_uris`, `release_date`, `streams`, `Source.Name`

## Coverage notes

- 2018-05-03 → 2026-10-15, 442 chart weeks, 200 rows per chart per week.
- The `GLOBAL` chart and Türkiye (`TR`) are present in all 442 weeks.
- The other 36 countries are present in 111 weeks. Compare countries with **Average Weekly Chart Streams**, not with raw totals.
- 13,450 rows have no `release_date`.

## Reproducing

Place the CSV files in a local folder and update the folder path in Power Query (**Transform data → Data source settings**). If you need to distribute the files, use Git LFS or link to the original source.
