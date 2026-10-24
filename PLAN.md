# Fog-of-War Chess — Project Plan

**Name:** Sai Rithwik Reddy Chirra  
**GitHub:** @imrithwik1908  
**Repository:** Private copy of `ARC-ASU/fog-of-war-project`  
**Course staff:** `@3rdAT`, `@Slash0BZ`

## 1. Starting point

I will start from the CNN agent included in `agents/baseline` and `submission/`. The main challenge is that the agent cannot see the full chessboard, so it needs to make reasonable moves even when enemy pieces are hidden.

I plan to run the supplied baseline against `bot:greedy` and `bot:guess-sf-4x500` and record its wins, draws, losses, and local Elo rating. I have **not run these matches yet**, so I am not reporting the example scores in the starter README as my own results.

```bash
python -m fow.arena agents/baseline bot:greedy bot:guess-sf-4x500 --games 100
python -m fow.validate submission
```

## 2. What I plan to try

**Idea 1 — Better use of past observations.** The starter agent has a basic record of last-seen enemy pieces. I want to test whether adding information about how recently a square was observed helps the network make better decisions under uncertainty. I will keep the rest of the model as similar as possible and compare it against the original baseline.

**Idea 2 — More varied training positions.** I will generate positions from games involving different reference bots, instead of relying only on the starter training set. Stockfish can provide labels **during training**, but the submitted agent will only use its own neural network to choose moves. I will compare the new model with Idea 1 and check whether performance improves beyond random match-to-match variation.

**Optional, if time allows — A small learned value head.** I may try predicting game outcomes from partial observations and use that prediction to compare candidate moves. I will only keep this if testing shows a real improvement without adding too much compute.

**How I will measure progress:** Play against the same reference bots with balanced colors and recorded seeds. Start with roughly 100–200 games per comparison; run more if the results are too close to distinguish. Record win/draw/loss, local rating and uncertainty, parameter count, and FLOPs per move. Change one component at a time.

## 3. Compute and reproducibility

I plan to use the ASU Sol class resources for data generation and PyTorch training. I will begin with small runs, record their actual time and GPU usage, and only scale up experiments that look promising. The submitted models will stay below the **250M-parameter** limit and **10^12 FLOPs per move**. I will run `fow.validate` before submitting an entry.

I will keep `JOURNAL.md` updated with commands, seeds, results and commit IDs. I will also maintain `REPRODUCE.md` and `reproduce.sh` so the final agent can be rebuilt from a fresh copy in hours, not days. AI assistance will be disclosed in `AI_USE.md`.

## 4. Risks and fallback

A full-board Stockfish move may depend on pieces the agent cannot see. More data might not fix that by itself. I will inspect losing games rather than assume a higher training accuracy means stronger play. If a new idea fails or takes too much compute, I will keep the strongest reproducible small CNN and document what I tested.

**Milestones:** Oct 23 — proposal; Nov 17 — first valid tournament entry; Dec 4 — final model; Dec 12 — report and recorded presentation.
