# Lakers Prop Tracker

I kept losing prop bets on Lakers games because I was going off intuition instead of actual data. So I built this.

It tracks the last 10 games for key Lakers players and calculates how often they hit their sportsbook prop lines — points, rebounds, assists. The goal was to figure out which players are actually *consistent* enough to bet on vs. which ones are a coin flip.

---

## What it does

- Logs each player's last 10 game stats alongside the prop lines I typically see on the book
- Calculates hit rate (% of games they went over the line) for pts, reb, and ast
- Measures a consistency score using coefficient of variation — basically how predictable their output is
- Surfaces the best bets: props with a 70%+ hit rate
- Generates a visual HTML dashboard to see it all at a glance

---

## Project layout

```
lakers-props/
├── data/
│   └── lakers_stats.py        ← game logs + prop lines per player
├── analysis/
│   └── analysis.py            ← hit rates, averages, consistency scores
├── visualizations/
│   └── dashboard.py           ← builds the HTML dashboard
└── README.md
```

---

## How to run it

Console output:
```bash
python analysis/analysis.py
```

Generate the visual dashboard:
```bash
python visualizations/dashboard.py
```
Then open `lakers_props_dashboard.html` in any browser.

No libraries needed — runs on plain Python 3.

---

## How I measure consistency

I use the **coefficient of variation** on points (std dev ÷ mean × 100). A lower CV means the player's output is tightly clustered around their average, which makes their props more predictable. The final score is just `100 - CV`, so higher = more consistent.

---

## Adding new games

Open `data/lakers_stats.py` and add a row to any player's game list:

```python
{"pts": 27, "reb": 8, "ast": 9, "min": 36, "opp": "GSW"},
```

Re-run the scripts and the numbers update automatically.

---

*For educational purposes only.*
