# YouTube Trailer Likes, Dislikes and Comment Mood vs IMDb Ratings (2012–2026)

Do people's reactions to a movie trailer on YouTube say anything about how good the movie turns out to be? One row per
film: 1,638 English-language films released 2012–2026, their most-viewed official YouTube trailer (views, likes,
dislikes, like ratio, comment sentiment) and the film's IMDb rating. Snapshot taken 2026-11-06.

## Sources

| Source | What it gives | License / terms |
| --- | --- | --- |
| [TMDB API](https://www.themoviedb.org/documentation/api) | Film list, release dates, genres, budget/revenue, IMDb IDs, the films' YouTube trailer IDs | Non-commercial use with attribution. This product uses the TMDB API but is not endorsed or certified by TMDB. |
| [IMDb non-commercial datasets](https://developer.imdb.com/non-commercial-datasets/) (`title.ratings.tsv.gz`) | IMDb rating and number of votes | Personal and non-commercial use. Information courtesy of IMDb (https://www.imdb.com). Used with permission. |
| [YouTube Data API v3](https://developers.google.com/youtube/v3) | Trailer views, likes, comment count, upload date, channel; the top comments (scored, never stored here) | YouTube API Services Terms. Only per-trailer aggregates are published, no comment text. |
| [Return YouTube Dislike API](https://returnyoutubedislike.com) | Dislike counts (YouTube hid them in Dec 2021) | Free public API, credited. Counts are archived (measured) or extrapolated (estimated), see Caveats. |
| [VADER](https://github.com/cjhutto/vaderSentiment) | Sentiment score of each comment | MIT |

## Files

- `trailers_vs_imdb.csv` (1,638 rows): one row per film.

How it was built: TMDB's 140 most-voted English films per release year (2012–2026) → films with ≥ 25,000 IMDb votes →
the most-viewed official YouTube trailer per film (≥ 1M views, likes and comments visible) → dislikes from Return
YouTube Dislike (≥ 2,000 likes + dislikes) → up to 300 top comments per trailer (YouTube's "Top comments" order),
English only (langdetect), at least 3 words, each scored with VADER.

## Data dictionary

### trailers_vs_imdb.csv

| Column | Type | Description |
| --- | --- | --- |
| `tmdb_id` | int | TMDB movie ID |
| `imdb_id` | string | IMDb title ID (`tt...`) |
| `title` | string | Film title (TMDB) |
| `release_date` | date | First release date (TMDB) |
| `release_year` | int | Year of `release_date` |
| `genres` | string | TMDB genres, `\|`-separated |
| `imdb_rating` | float | IMDb average rating, 1–10 |
| `imdb_votes` | int | Number of IMDb votes |
| `youtube_video_id` | string | The trailer's YouTube ID (`https://www.youtube.com/watch?v=<id>`) |
| `trailer_title` | string | The trailer's YouTube title |
| `trailer_channel` | string | YouTube channel that posted it |
| `trailer_upload_date` | date | Upload date |
| `trailer_views` | int | Views at snapshot |
| `trailer_likes` | int | Likes at snapshot (YouTube, exact) |
| `trailer_dislikes` | int | Dislikes at snapshot (Return YouTube Dislike) |
| `dislikes_source` | string | `measured` = trailer uploaded before 2021-12-13, dislike count archived from YouTube; `estimated` = uploaded later, extrapolated from extension users |
| `like_ratio_pct` | float | likes / (likes + dislikes) × 100 |
| `trailer_comment_count` | int | Total comments on the trailer (YouTube) |
| `comments_scored` | int | Top comments that passed the filters and were scored (max 300) |
| `comments_positive_pct` | float | % of scored comments VADER rates positive (compound ≥ 0.05); empty if fewer than 50 scored |
| `comments_negative_pct` | float | % negative (compound ≤ −0.05) |
| `comments_neutral_pct` | float | % neutral |
| `comment_mood` | float | positive % − negative %, −100 to +100 |
| `budget_usd` | int | Budget (TMDB, often missing) |
| `revenue_usd` | int | Worldwide box office (TMDB, often missing) |
| `snapshot_date` | date | Day the YouTube/RYD/IMDb numbers were read |

## Key figures (from the data)

- Like ratio vs IMDb rating: Spearman 0.33 (0.36 for measured dislikes only, 0.35 for estimated only).
- Trailers in the most-liked quarter (median 98.1% liked) average **6.9** on IMDb; the least-liked quarter (median 89.8%)
  averages **6.1**. 46% of most-liked-quarter films score 7+, vs 19% of least-liked-quarter films.
- Comment mood vs like ratio: Spearman 0.21 (1,529 films with ≥ 50 scored comments). Comment mood vs IMDb: 0.24.
- The Odyssey (2026): 77.3% liked (bottom 4% of all trailers, estimated dislikes), IMDb 8.4.

## Caveats

- **Dislikes after Dec 2021 are estimates.** Return YouTube Dislike extrapolates them from its extension users, who are
  not a random sample of viewers. Even "measured" counts have extension-based changes added since 2021.
- **Everything is measured today, not at release.** Likes, dislikes and comments keep accumulating, and IMDb ratings
  of recent films (2025–2026) still move.
- **Dislikes are not only about quality.** The lowest ratios (Snow White, Ghostbusters 2016, The Little Mermaid, The
  Woman King) were organised dislike campaigns over casting or politics.
- **VADER reads words, not meaning.** It misses sarcasm and reads hype as negative ("this is insane", "I'm crying",
  "Kong is going to kill him"): e.g. Spider-Man: No Way Home and Godzilla vs. Kong get negative comment moods while
  their trailers are 98–99% liked.
- **Top comments are fans and jokes**, not the average viewer; only English comments are scored.
- One trailer per film (the most-viewed official one); other trailers of the same film can differ.
- Trailers showing 0 likes on YouTube (a glitch, e.g. Speak No Evil 2024) are left out.

## Dashboard ideas

- Like ratio (x) vs IMDb rating (y), one dot per film, coloured by measured/estimated.
- Average IMDb rating per like-ratio quarter (bars).
- "Hated trailer, loved movie" and "loved trailer, flop" lists (biggest gaps from the trend).
- Comment mood vs like ratio by genre: are horror and action comments read as "negative" by VADER?
