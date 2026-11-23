# What Makes a Steam Game a Hit? 8,000 Games

> **Synthetic dataset.** Every row was generated with Python to mimic Steam-style PC games. It contains no real games and no personal data. Patterns reflect how the generator was built, not the real world.

## What is this?

A video game dataset with a clear prediction target. **8,000 rows, 22 columns, one CSV (~768 kB).** `hit` = 1 if the game is in the top 20% of `revenue_musd`.

## Why should you use it?

- **Clean, complete data**: no missing values, no joins needed
- **Two targets**: `hit` (classification) and `revenue_musd` (regression)
- **Leakage practice**: outcome columns are clearly separated so you can practice avoiding target leakage
- **Fast to start, still interesting**: nonlinear effects, interactions and noise, so tuned models beat simple baselines
- **Universal appeal**: everyone has an opinion on what makes a hit

## Columns

| Column | Type | Description |
|--------|------|-------------|
| `game_id` | int | Unique identifier |
| `title` | int | Synthetic game title |
| `genre` | int | Primary genre (12 categories) |
| `release_year` | int | Release year (2012-2025) |
| `is_indie` | int | 1 if made by a small indie team |
| `team_size` | int | Developers on the team |
| `price_usd` | float | Launch price in USD (0 = free) |
| `has_multiplayer` | int | 1 if the game has multiplayer |
| `early_access` | int | 1 if launched in early access |
| `controller_support` | int | 1 if full controller support |
| `languages_supported` | int | Number of UI languages |
| `dlc_count` | int | Number of DLC packs |
| `file_size_gb` | float | Install size in GB |
| `metacritic_score` | int | Critic score (30-97) |
| `steam_positive_pct` | int | % of positive user reviews |
| `wishlists_k` | float | Pre-launch wishlists (thousands) |
| `trailer_views_k` | float | Trailer views (thousands) |
| `num_reviews` | int | Total user reviews (post-launch outcome) |
| `owners_k` | float | Estimated owners in thousands (outcome) |
| `peak_concurrent_players` | int | Peak concurrent players (outcome) |
| `revenue_musd` | float | Lifetime revenue in USD millions (regression target) |
| `hit` | int | **Classification target**: 1 if top-20% revenue |

**Outcome columns (do not use as features when predicting `hit`):** `num_reviews`, `owners_k`, `peak_concurrent_players`, `revenue_musd`, `hit`

## Suggested Tasks

- **Classification:** predict `hit` from launch-time features (drop outcome columns to avoid leakage)
- **Regression:** predict `log(revenue_musd)`
- **Analysis:** does a high wishlist count or a high review score matter more?
- **Genre study:** which genres have the highest hit rate, and has that changed since 2012?
- **Pricing:** is there a price sweet spot for indie vs. AAA games?

## Quick Start

```python
import pandas as pd

df = pd.read_csv("steam_game_hits.csv")
print(df.shape)
print(f"Positive rate of hit: {df['hit'].mean():.1%}")

outcomes = ['num_reviews', 'owners_k', 'peak_concurrent_players', 'revenue_musd', 'hit']
X = df.drop(columns=['game_id', 'title'] + outcomes)   # 15 launch-time features
y = df["hit"]
```

## How the data was generated

A hidden "quality" variable plus marketing/context variables drive the features, and the outcomes follow from them through logistic and log-normal relationships with random noise. Random seed: 1501. Treat conclusions as properties of the generator, which makes this a good sandbox for practicing modelling, EDA and evaluation.

## License

CC0 Public Domain
