# Hill Rush

A 2D motocross racing game that runs in any modern browser. It's a single `index.html` file with no build step and no dependencies.

## Play

Open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8000
```

Then visit http://localhost:8000.

## Controls

| Action        | Keyboard          | Touch |
|---------------|-------------------|-------|
| Throttle      | ↑ / W / Space     | ▶     |
| Brake         | ↓ / S             | ◼     |
| Lean back     | ← / A             | ↺     |
| Lean forward  | → / D             | ↻     |
| Restart       | R                 |       |
| Pause         | Esc / P           | ❚❚    |
| Mute          | M                 | 🔊    |

## Features

- Physics-based bike: two wheels plus the rider, terrain collision, and weight shifting when you lean.
- Three procedurally generated tracks (Easy, Medium, Hard) with day, sunset and night themes.
- Three AI rivals, checkpoints, crashes and respawns.
- Flip bonuses: every full flip you land takes 1 second off your time.
- Best times saved in your browser, synthesized engine sound, and touch controls on mobile.
