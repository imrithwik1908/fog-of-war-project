# Project Journal

## October 23, 2026 — Initial plan

**Goal:** Set up the starter project and establish a baseline before changing the model.

**What I did:** Created a private copy of the course repository and drafted an initial plan. My first experiments will focus on better use of visible/last-seen information and more varied training positions.

**Baseline status:** Not run yet. I will record results only after running the matches myself.

**Planned commands:**
```bash
python -m fow.arena agents/baseline bot:greedy bot:guess-sf-4x500 --games 100
python -m fow.validate submission
```

**Next steps:** Confirm staff access, run the baseline, note its local Elo and match results, and record the commit ID, seed, commands, and runtime for each experiment.

**AI use:** ChatGPT assisted with the wording of the initial project documents; see `AI_USE.md`.
