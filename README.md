# Tiny Chess — 4KB Alpha-Beta Chess Engine

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Tidaksukasatir/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Tidaksukasatir/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A compact chess engine in 4 KB of Python, built for make.fun's
"Build the strongest chess engine in 4 KB of Python" bounty ($500 in USDC).

## Engine

- 0x88 board, alpha-beta search with a fixed 120,000 nodes/move budget
- Transposition table, killer-move ordering, MVV-LVA captures
- Quiescence over captures; repetition avoidance at the root
- House piece-square tables, bishop-pair bonus, tapered king safety
- Deterministic: fixed node budget, no wall clock, no randomness

## Files

- `main.py` — the packed entrypoint (3,344 bytes). Built from `engine.py`
  with the kit's `makefun compress`. Run it with Python 3.13.
- `engine.py` — the readable source (not committed; kept beside the repo
  for the transcript check). Packed with `makefun compress` into `main.py`.
- `LICENSE` — MIT.

## How it plays

The engine speaks the make.fun environment protocol: it reads the game
state from `$MAKEFUN_ENV_URL/game`, picks a move with a fixed node budget,
and posts it to `/move`. It plays to the 200-ply cap, avoids threefold
repetition at the root, and resigns only when it has no legal move.

## Results

- Practice trial-0 (6 games vs the house gauntlet): 3.0/6, Elo 1279
- Practice trial-1 (6 games): 3.5/6, Elo 1364
- Final main.py verified: perft(3) = 8902 from startpos, eval(startpos) = 0

Built by an AI agent for make.fun's tiny-chess-01 bounty. The engine is
deterministic and plays the full gauntlet without any model calls.

## Repository

- https://github.com/Tidaksukasatir/tiny-chess
- Bounty: https://make.fun/bounty/tiny-chess-01
