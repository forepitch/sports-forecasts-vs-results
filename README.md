# Forepitch: sports match forecasts vs results

This is every pre-match forecast published by the [Forepitch](https://forepitch.com/) statistical model since 28 September 2026, each paired with the final result: **6,849 matches in six sports** (football, hockey, tennis, basketball, volleyball and MMA).

Each row holds the last estimate published before kick-off. No row is removed or edited after the result is known.

- **Live data, updated daily:** https://forepitch.com/data/forepitch-record.csv
- **Accuracy by sport and league:** https://forepitch.com/accuracy/
- **On Kaggle:** [dataset](https://www.kaggle.com/datasets/forepitch/sports-match-forecasts-vs-results-forepitch) and [notebook](https://www.kaggle.com/code/forepitch/sports-forecasts-calibration-and-brier-score)

## Files

| Path | What it is |
|---|---|
| [`data/forepitch-record.csv`](data/forepitch-record.csv) | One row per finished match: probabilities, most likely outcome and score, final score |
| [`data/competitions.csv`](data/competitions.csv) | Full English name and country for each competition code |
| [`notebooks/calibration.ipynb`](notebooks/calibration.ipynb) | Calibration plots, Brier score, log loss and accuracy by league |

### `forepitch-record.csv`

| Column | Meaning |
|---|---|
| `kickoff_utc` | Kick-off time (UTC) |
| `estimate_utc` | When the forecast was made (UTC); this is the last estimate before kick-off |
| `sport` | One of `football`, `hockey`, `tennis`, `basketball`, `volleyball`, `mma` |
| `competition` | Competition code; full names are in `competitions.csv` |
| `home`, `away` | The two teams. In tennis and MMA, `home` is the first-listed player |
| `p_home`, `p_draw`, `p_away` | Probability of each outcome. In hockey these are for regulation time. `p_draw` is empty for sports without draws |
| `pick`, `pick_p` | The most likely outcome (`h`, `d` or `a`) and its probability. In hockey this is the match winner, including overtime |
| `likely_score` | The single most likely score (football and hockey only) |
| `final_score` | The final score. In hockey it includes overtime; a game decided by a shootout can show a level score |
| `pick_hit`, `score_hit` | `1` if the most likely outcome / score happened, otherwise `0` |
| `url` | The match page with the full forecast |

## Snapshot (to 17 November 2026)

| Sport | Matches | Most likely outcome happened |
|---|---|---|
| Football | 3,238 | 53.2% |
| Hockey | 1,539 | 60.1% |
| Tennis | 987 | 64.2% |
| Basketball | 663 | 69.7% |
| Volleyball | 369 | 81.3% |
| MMA | 53 | 64.2% |

### Football against a baseline

The baseline uses the overall frequencies of home wins, draws and away wins, so it knows nothing about the teams.

| Measure | Model | Baseline |
|---|---|---|
| Brier score (1X2) | 0.580 | 0.648 |
| Log loss | 0.974 | 1.070 |

### Calibration

When the model gives an outcome 60–70%, it happens 67.8% of the time. When it gives 70–80%, it happens 79.0% of the time. The notebook has the full reliability diagram.

## License

The data is released under [CC BY 4.0](LICENSE). You can use it for any purpose, as long as you credit **Forepitch** with a link to https://forepitch.com/.

These are a statistical model's estimates, published for analysis. They are not advice of any kind.
