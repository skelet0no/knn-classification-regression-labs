# Datasheet: What Makes a Steam Game a Hit? 8,000 Games

## Motivation

**What is this dataset for?**
Practicing classification, regression and exploratory analysis on Steam-style PC games. Primary target `hit`; secondary target `revenue_musd`.

**Why was it created?**
Many public tabular datasets lack a clean target or are full of missing values. This one is complete, documented and leakage-aware.

## Composition

**What do the instances represent?**
Each row is one synthetic video game. No real entities are described.

**How many instances?** 8,000

**What data does each instance consist of?**
22 columns: identifiers (game_id, title), features, outcome columns (num_reviews, owners_k, peak_concurrent_players, revenue_musd, hit).

**Is there a label or target?**
Yes. `hit` is binary (20.0% positive); `revenue_musd` is continuous and right-skewed (log-transform recommended).

**Missing data?** None.

**Recommended splits:** random stratified split on `hit`; rows are independent.

## Collection Process

**How was the data created?**
Synthetically generated with NumPy/pandas (seed 1501). A latent quality variable and context variables drive the features; outcomes are derived with logistic / log-normal links plus noise. `hit` = 1 if the game is in the top 20% of `revenue_musd`.

## Preprocessing

None. Data is generated in its final format.

## Uses

**Suitable:** teaching, benchmarking, notebooks, EDA practice, evaluating leakage-awareness.
**Not suitable:** drawing conclusions about real games, real-world forecasting, or commercial decisions.

## Limitations

Relationships are programmatic and cleaner than real-world data. Names are random and not real. Outcome columns are deterministic-ish functions of the latent variables, so do not use them as features for `hit`.

## Distribution and License

CC0 Public Domain.

## Maintenance

Maintained by the author on Kaggle (vedauv).
