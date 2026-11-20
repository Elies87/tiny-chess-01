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

## Verification (local, before submission)

- Size: `main.py` is 3,991 bytes (limit 4,096); the whole repository is
  5,812 bytes (limit 8,192).
- Legality: perft counts match the known values on six standard test
  positions, including Kiwipete, through the exact committed file.
- Determinism: the same position evaluated in two separate processes
  returns the identical move; the search budget is a fixed 65,000 nodes,
  never the clock.
- Strength: in the kit's official practice gauntlet (trial 0) the engine
  scored 3.5/6 — checkmate wins over the 855, 1073 and 1596 anchors and a
  draw — for an estimated rating of about 1,365, above the 1,154 needed
  to reach the final. The prize bar (beating the house 4 KB baseline in
  the final) can only be settled by the official grading.

## Design notes

The board uses a 0x88 representation. Evaluation is my own: material,
piece-square tables for every piece, pawn-structure terms (doubled and
passed pawns), a bishop-pair bonus, and a king-safety/endgame blend driven
by the remaining material. Fitting the 4 KB cap cost the readable version
its history heuristic, isolated-pawn penalty and open-file rook bonus
(about 30–80 Elo in local testing); the fixed node budget was chosen so
the engine answers in roughly 1.3–3.0 seconds a move on one core, inside
the 10-second limit, with no clock dependence anywhere.

License: MIT (see LICENSE).
