# TD-Matrix: NFL Anytime Touchdown Predictor

Predicts the probability that each QB, RB, WR, and TE scores an **anytime touchdown** (rushing, receiving, or return; passing TDs don't count) in that week's games. Predictions are made on Wednesday, using only information available before the game.

This is a learning project. Each step is a notebook that explains the ML ideas as it goes.

## Roadmap

| Step | Notebook | What it covers |
|---|---|---|
| 1 | `notebooks/01_build_player_game_dataset.ipynb` | One row per player per game, the ATTD label, backwards-looking features, data leakage |
| 2 | *coming next* | Baseline, logistic regression and LightGBM, time-based validation, log loss, calibration |
| 3 | *planned* | Comparison against sportsbook ATTD odds, expected value, backtesting |
| 4 | *planned* | Streamlit app that refreshes every Wednesday |

`nfl_touchdown_predictor.ipynb` is the original season-level QB exploration, kept for reference.

## How we measure success

About 21% of player-games include a touchdown, so a model that always says "no" is ~79% accurate and worthless. We judge models by **log loss / Brier score**, **calibration**, and (Step 3) **edge versus sportsbook odds**.

## Data

- `data/play_by_play_{2023,2024,2025}.csv`: nflverse play-by-play (2025 currently through week 12)
- `data/roster_{2023,2024,2025}.csv`: nflverse rosters, used for player positions ([source](https://github.com/nflverse/nflverse-data/releases/tag/rosters))
- `data/player_games.parquet`: output of Step 1

## Known simplifications

- A player is counted as "playing" if they had at least one carry, target, or pass attempt.
- `spread_line` / `total_line` are closing lines, which move slightly after Wednesday.

## Setup

```bash
pip install -r requirements.txt
cd notebooks && jupyter notebook
```
