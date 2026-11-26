# Business insights

All figures come from the Power BI model with **no filters applied** (all 442 chart weeks, 2018-05-03 → 2026-10-15), unless noted otherwise.

> **Coverage caveat.** The Global chart and Türkiye have weekly data (442 weeks). The other 36 countries have 111 weeks. Raw country totals therefore overstate Türkiye by roughly 4×. Use *Average Weekly Chart Streams* for country comparisons.

## 1. The US, Mexico and Brazil generate the most chart streams per week

Average weekly Top 200 chart streams, all countries except Global:

| Rank | Country | Avg weekly chart streams |
|---|---|---|
| 1 | US | 624.5 M |
| 2 | Mexico | 357.4 M |
| 3 | Brazil | 336.2 M |
| 4 | Germany | 167.4 M |
| 5 | UK | 155.4 M |
| 6 | Spain | 143.0 M |
| 7 | Türkiye | 129.6 M |
| 8 | Italy | 128.3 M |

On raw totals, Türkiye ranks 2nd (57.3 bn), behind the US (69.3 bn). Once the extra weeks of coverage are accounted for, it falls to 7th.

## 2. Long-running hits dominate chart entries

Tracks with the most chart entries, counted across all 37 countries plus Global (by `track_id`):

1. *Blinding Lights*, The Weeknd: 2,235 entries, charted in all 37 countries
2. *Someone You Loved*, Lewis Capaldi: 2,011
3. *Another Love*, Tom Odell: 1,939
4. *lovely*, Billie Eilish & Khalid: 1,902
5. *Shallow*, Lady Gaga & Bradley Cooper: 1,562

## 3. The biggest artists in the charts

Top artists by Global chart streams, using the artist bridge. Each collaborating artist gets the full streams of a joint track.

| Rank | Artist | Global chart streams | Chart entries (all charts) | Songs |
|---|---|---|---|---|
| 1 | Bad Bunny | 42.5 bn | 17,990 | 201 |
| 2 | The Weeknd | 29.5 bn | 12,038 | 111 |
| 3 | Taylor Swift | 26.1 bn | 7,667 | 235 |
| 4 | Billie Eilish | 22.9 bn | 11,567 | 60 |
| 5 | Drake | 20.7 bn | 11,836 | 260 |
| 6 | Bruno Mars | 18.4 bn | 4,808 | 41 |
| 7 | Justin Bieber | 18.2 bn | 7,640 | 118 |
| 8 | Post Malone | 17.8 bn | 9,244 | 83 |
| 9 | Ariana Grande | 17.1 bn | 6,947 | 112 |
| 10 | Ed Sheeran | 14.2 bn | 8,335 | 98 |

There are 22,800 individual artists across all charts (7,323 in 2024 alone). In the US chart, Drake ranks first.

## 4. Weeks at No. 1 on the Global chart

Counted by song (title + artists), so a song released under more than one track ID is counted once:

| Song | Artists | Weeks at #1 |
|---|---|---|
| Die With A Smile | Lady Gaga, Bruno Mars | 30 (split 21 + 9 across two track IDs) |
| Dance Monkey | Tones And I | 17 |
| Señorita | Shawn Mendes, Camila Cabello | 14 |
| Blinding Lights | The Weeknd | 13 |
| All I Want for Christmas Is You | Mariah Carey | 13 |
| The Fate of Ophelia | Taylor Swift | 12 |
| STAY | The Kid LAROI, Justin Bieber | 12 |
| Flowers | Miley Cyrus | 12 |

About 14% of track IDs are duplicates of the same song (81,010 IDs → 69,883 songs). Counting by `track_id` alone splits runs like *Die With A Smile*'s, so the report counts songs with `DimTrack[SongKey]`.

## 5. Chart streams grew steadily until 2024

| Year | Global chart streams | Country chart streams | Chart weeks |
|---|---|---|---|
| 2018* | 57.9 bn | 20.7 bn | 35 |
| 2019 | 90.0 bn | 33.8 bn | 52 |
| 2020 | 96.6 bn | 35.9 bn | 53 |
| 2021 | 98.3 bn | 38.2 bn | 52 |
| 2022 | 105.7 bn | 44.2 bn | 52 |
| 2023 | 128.9 bn | 55.5 bn | 52 |
| 2024 | 148.0 bn | 62.7 bn | 52 |
| 2025 | 136.8 bn | 59.8 bn | 52 |
| 2026* | 105.4 bn | 47.2 bn | 42 |

\* partial years. Global Top 200 streams rose about 64 % from 2019 to 2024, then fell about 8 % in 2025.

## 6. Europe has the most countries; North America has the most streams per country

| Continent | Countries | Country chart streams |
|---|---|---|
| Europe | 22 | 123.1 bn |
| North America | 3 | 119.0 bn |
| South America | 5 | 70.8 bn |
| Asia | 3 | 68.3 bn |
| Oceania | 2 | 12.1 bn |
| Africa | 2 | 4.8 bn |


## 7. Ranks drift downward from week to week

Across rows with a previous rank, *Average Rank Improvement* is **−18.0**. That means tracks still in the chart fall about 18 places a week on average. New entries and re-entries have no previous rank, so they are excluded; the positions they take are what push other tracks down.

## Validation checks performed

- `DimCountry[CountryCode]` is unique (38 codes), with no blank names or continents.
- Every `FactSpotify[CountryCode]` matches `DimCountry`, and no fact rows have a blank code.
- Each chart has exactly 200 rows per week, with no duplicate (week, rank) pairs.
- The Global chart is excluded from the map and from Country Chart Streams.
- Track counts use `track_id`; song counts use `SongKey`, so duplicate track IDs are merged.
- Artist counts use the split artist bridge, never the unsplit `artists` text.
- 13,450 rows with a missing `release_date` are left blank, not filled in.
