# tiny-chess-01 entry

An original chess engine in a single Python file (stdlib only), built for the
make.fun tiny-chess-01 bounty: negamax alpha-beta search with iterative
deepening under a fixed node budget (fully deterministic), quiescence search,
transposition table, null-move pruning, late move reductions, killer and
history move ordering, and a hand-tuned evaluation (material, piece-square
tables, pawn structure, bishop pair, king safety/endgame blend).

`main.py` is a self-contained compressed payload (lzma + base85, as the
starter README allows): it decompresses and runs the engine source in memory.
The engine talks to the environment at `MAKEFUN_ENV_URL`, requests the
current game, and replies with UCI moves.

License: MIT (see LICENSE).
