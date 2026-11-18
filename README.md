# Kart Cup Commissioner

A single-page web app that runs a Mario Kart tournament night: enter the names, race,
tap in the finishing order, and the app handles seeding, lobbies, shuffling and the podium.

Open `index.html` in a browser. No build step, no dependencies, no server required —
everything is in that one file, and progress is saved to the browser's local storage so you
can close the tab mid-tournament and pick it back up.

To serve it over HTTP instead (useful if several people want it on their phones over the
same wifi):

```bash
python3 -m http.server 8787
```

## How the tournament runs

1. **The grid.** Enter every racer. Any number from 3 up works — the app splits the field
   into lobbies of 4 where it can, falling back to 3s and 5s so nobody is left in a lonely
   pair. 10 racers becomes 4/3/3; 13 becomes 5/4/4.
2. **Pool play.** Two quick mixed races (configurable). Heats are drawn so you face
   different people in each one. These points **only set the seeding** — they don't decide
   the title.
3. **Divisions.** Seeds are slotted top-down: seeds 1–4 open in the Rainbow Division, the
   next four in Star, and so on.
4. **Rounds.** Three rounds of four races each, by default. Points per race follow the
   in-game table: **15 / 12 / 10 / 9** for 1st through 4th (5th gets 8).
5. **The shuffle.** After every round the top finishers in each lobby move up a division
   and the bottom finishers drop one. Neighbouring lobbies always swap the same number of
   racers, so lobby sizes never drift.
6. **The cup.** Final standings follow your division and your placing in the final round,
   so the champion comes out of the last Rainbow Division race. Total points are shown
   throughout as bragging rights and as a tiebreak.

Tiebreaks, in order: round points, race wins in the round, total points, best single finish.

## What's in the app

- Tap-in-order result entry sized for a phone, with undo and edit-after-the-fact
- Live division boards showing who is currently promoting (▲) and relegating (▼)
- A suggested track per race, with a reroll button, that avoids repeating tracks
- Standings panel: pool points, main points, total, wins, average finish, races
- Podium with confetti, plus awards for most wins, hottest round, points leader and
  biggest climb from seeding
- Copy-results button for pasting the final classification into a group chat

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole app — markup, styles and tournament engine |
| `.claude/launch.json` | Dev-server config for the Claude Code browser pane |
