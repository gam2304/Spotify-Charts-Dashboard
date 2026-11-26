# Data dictionary

## FactSpotify, one row per track per chart per week

| Column | Type | Description |
|---|---|---|
| week_end | Date | Last day of the chart week. Relates to `DimDate[Date]` |
| CountryCode | Text | Chart code (ISO-2 country code, or `GLOBAL`). Relates to `DimCountry` |
| rank | Whole number | Chart position this week (1–200) |
| prev_rank | Whole number | Position in the previous chart week; blank for new entries and re-entries |
| peak | Whole number | Best position the track has reached in that chart |
| appearances | Whole number | Number of weeks the track has appeared in that chart |
| entry_status | Text | Movement status supplied with the source data |
| track_id | Text | Spotify track ID. Use this, not `title`, to count tracks |
| title | Text | Track title. Not unique: different tracks can share a title |
| artists | Text | All credited artists in one text value, separated by `\|` |
| artist_uris | Text | Spotify artist URIs matching `artists` |
| release_date | Date | Track release date (13,450 rows blank) |
| streams | Whole number | Streams counted for the track in that chart week |
| Source.Name | Text | Source CSV file name |

## DimCountry

| Column | Description |
|---|---|
| CountryCode | Unique key (38 rows: 37 countries + `GLOBAL`) |
| CountryName | Country name; data category **Country/Region**. `Global` for the worldwide chart |
| ContinentName | Continent; data category **Continent**. `Global` for the worldwide chart |
| MapName | Calculated column: CountryName as spelled in the world-atlas map file (US → United States of America, UK → United Kingdom, Türkiye → Turkey). Used by the Shape Map |

## DimContinent

| Column | Description |
|---|---|
| ContinentCode | Two-letter continent code |
| ContinentName | Continent name (key to `DimCountry[ContinentName]`). `SA` is renamed from `America` to `South America` |

## DimDate (Power Query; marked as date table)

| Column | Description |
|---|---|
| Date | One row per day from the first to the last `week_end` |
| Year | Calendar year |
| MonthNumber | 1–12 |
| MonthName | English month name; sorted by MonthNumber |
| YearMonth | `yyyy-MM` |
| Quarter | `Q1`–`Q4` |

## DimTrack (Power Query, from FactSpotify)

| Column | Description |
|---|---|
| track_id | Unique Spotify track ID (81,010 rows) |
| title | Track title |
| artists | Credited artists, `\|`-separated |
| SongKey | `lower(title) \| lower(artists)`: merges the same song released under several track IDs (69,883 distinct) |
| Song | Display label `title - artist, artist` used in the Top 10 songs chart |

## BridgeTrackArtist (Power Query, from FactSpotify)

One row per track per credited artist (134,005 rows).

| Column | Description |
|---|---|
| track_id | Key to `DimTrack` |
| ArtistKey | Spotify artist URI (or `name:<artist>` when no URI is given; 1 case) |
| artist_name | Artist name as written on that track |
| artist_position | 1 = first credited artist |

## DimArtist (Power Query, from BridgeTrackArtist)

| Column | Description |
|---|---|
| ArtistKey | Unique artist key (22,800 artists) |
| Artist | Artist name |

## CountryLookup

A reference table (Continent, CountryCode, CountryName) used to enrich `DimCountry`. It has no relationships in the model.

## _Measures

See the measure table in the main `README.md`.
