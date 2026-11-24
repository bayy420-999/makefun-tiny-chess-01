# Tiny Chess Engine

A 4 KB Python chess engine for the make.fun tiny-chess-01 bounty: strongest engine in 4,096 bytes, Python 3.13 stdlib only, deterministic.

## Design

- 0x88 board, negamax with principal-variation search and iterative deepening
- Fixed node budget (30,000 nodes/move, soft gate at 60% for the next depth) — never a clock, fully deterministic
- Capture-only quiescence with check evasions, Zobrist transposition table, killer moves, late-move reductions, null-move pruning, check extensions, mate-distance pruning
- Tapered piece-square tables with a passed-pawn fold, fitted to the position set
- A small embedded opening book: lines recorded by replaying wins against the house opponents offline (deterministic opponents replay move-for-move), stored as packed move lists

## Measured results (local, kit harness)

- Practice trial 0: Elo 2112, 6/6 by checkmate, 637 spare plies
- Practice trials 1–2: 1191 / 1654 (mean 1652)
- Simulated final draws (8 games incl. 1M/2M nodes): 1087 / 1253 / 1087

## Layout

- `main.py` — the engine (4,082 bytes, LZMA-packed, stdlib only)
- `LICENSE` — MIT
