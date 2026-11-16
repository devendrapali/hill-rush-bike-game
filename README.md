# Hill Rush

A 2D motocross racing game that runs in any modern browser. Race three computer-controlled riders over hills, jumps and drops. Land your jumps cleanly, and pull off flips to cut time off your run.

The whole game is a single `index.html` file. It needs no build step, no dependencies and no internet connection. Everything, including the graphics and engine sound, is generated in code.

---

## Quick start

### Option 1: Open the file

Download or clone the repository and double-click `index.html`. It opens in your default browser.

### Option 2: Run a local server

From the project folder:

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000 in your browser.

### Option 3: Host it online

Because it's a single static file, you can host it anywhere that serves HTML, such as GitHub Pages, Netlify or Vercel. For GitHub Pages, go to **Settings → Pages**, choose your branch and the root folder, and save. The game will be live at `https://<your-username>.github.io/<repo-name>/`.

---

## Controls

| Action       | Keyboard      | Touch screen |
|--------------|---------------|--------------|
| Throttle     | ↑ / W / Space | ▶            |
| Brake        | ↓ / S         | ◼            |
| Lean back    | ← / A         | ↺            |
| Lean forward | → / D         | ↻            |
| Restart race | R             | (pause menu) |
| Pause        | Esc / P       | ❚❚           |
| Mute sound   | M             | 🔊           |

On phones and tablets the touch buttons appear automatically. The left pair controls lean and the right pair controls brake and throttle. Landscape orientation gives the widest view.

---

## How to play: tutorial

### 1. Pick a track

The main menu lists three tracks along with your best time on each. Click or tap one to start.

### 2. The start

You start at the back of a four-bike grid. A **3 – 2 – 1** countdown plays, then **GO!** Hold the throttle as soon as GO appears.

### 3. Riding basics

- **Throttle** drives the rear wheel. The bike speeds up on flat ground and can climb steep hills, but it slows down on the way up.
- **Brake** slows both wheels. Use it to control your speed before a big jump so you don't overshoot the landing.
- **Leaning** rotates the bike:
  - **Lean back (←)** lifts the front wheel. Use it to pop a wheelie, to avoid landing nose-first, or to rotate backwards in the air.
  - **Lean forward (→)** drops the front wheel. Use it to stop the bike flipping over backwards on steep climbs, or to rotate forwards in the air.
- The rider shifts their weight when you lean. Leaning also works on the ground, not just in the air.

### 4. Jumps and landings

- Match the bike's angle to the slope you're landing on. Landing with both wheels parallel to the ground keeps your speed.
- Landing on the back wheel first is fine. Landing nose-first or upside down is not.
- If you take off too steep, tap **lean forward**. If the nose is dropping, tap **lean back**.
- When you're not pressing a lean key, a **stability assist** gently levels the bike. It's strongest on Easy and weakest on Hard, so you need to steer the bike yourself on harder tracks.

### 5. Crashes and checkpoints

- If your **helmet hits the ground**, you crash.
- About 1.5 seconds after a crash, you respawn at the **last checkpoint you passed**, standing still. The race clock keeps running, so crashes cost you time.
- Checkpoints are the **yellow flags** along the track, and they turn green once you pass them. The progress bar at the top of the screen shows where they are.

### 6. Flips = time bonus

- Make a **full 360° rotation** in the air, forwards or backwards, and land it without crashing.
- Each flip you land takes **1.0 second** off your final time. A double flip takes off 2 seconds.
- Flips that end in a crash earn nothing.

### 7. Finishing

- Cross the checkered **FINISH** gantry to finish the race.
- The results screen shows the final standings, your flip count and time bonus, your number of crashes, and whether you set a new personal best.
- From the results screen you can **Retry**, go to the **Next track**, or return to the **Menu**.

---

## The heads-up display

| Where          | What it shows                                                        |
|----------------|----------------------------------------------------------------------|
| Top left       | Race time (with flip bonuses already subtracted), track name, current position (P1–P4) |
| Top centre     | Progress bar: every rider's position, plus checkpoint markers        |
| Top right      | Mute and pause buttons                                               |
| Bottom right   | Speed in km/h                                                        |
| Centre         | Countdown and pop-up messages (CHECKPOINT, FLIP, CRASH, FINISH)      |

---

## Tracks

| Track          | Difficulty | Setting | What to expect                                                    |
|----------------|------------|---------|-------------------------------------------------------------------|
| Green Valley   | Easy       | Day     | Gentle rolling hills and small table-top jumps. Strong stability assist. |
| Canyon Run     | Medium     | Sunset  | Steeper hills, bigger jumps and step-down drops. Faster rivals.  |
| Midnight Ridge | Hard       | Night   | Big air, steep climbs and long drops. Weak assist and the fastest rivals. You'll need to use lean. |

The tracks are generated from fixed seeds, so each track is the same every time you play it. That way you can learn a track and improve your time.

---

## Rivals

| Rider | Colour |
|-------|--------|
| Blaze | Red    |
| Volt  | Blue   |
| Moss  | Green  |

The rivals ride with the same physics as you. They lean to match the ground ahead, and they can crash too. They get faster as the tracks get harder. On Hard, you'll usually need clean landings and a few flip bonuses to win.

---

## Tips

1. **Don't hold lean all the time.** Short taps give finer control than holding the key down.
2. **Ease off the throttle before huge jumps** if you keep overshooting the landing slope.
3. **Lean forward on steep climbs** to stop the bike flipping over backwards.
4. **Backflips are easiest off big kickers.** Lean back as soon as you leave the ramp, then let go as the bike comes around.
5. **A safe landing beats a risky flip.** One crash costs more time than a flip saves.

---

## Saved data

The game stores your best time on each track and your mute setting in your browser's `localStorage`. It saves nothing anywhere else. To reset your best times, clear the site data for the page in your browser.

---

## Technical overview

- **Rendering:** HTML5 Canvas 2D, scaled for high-resolution screens, with layered scrolling backgrounds and a camera that follows your bike and zooms out at speed.
- **Physics:** each bike is three points (rear wheel, front wheel and rider) held together by distance constraints. The game updates them in fixed steps of 1/240 s. The wheels collide with the terrain and grip it, throttle drives the rear wheel, and leaning pushes the wheels in opposite directions to rotate the bike.
- **Terrain:** generated from a seeded random-number generator out of building blocks (rolling hills, climbs, bumps, table-top jumps and step-down drops), then smoothed.
- **Rivals:** controlled by a simple rule that leans each bike towards the angle of the ground ahead of it.
- **Audio:** generated live with the Web Audio API (engine sound, countdown beeps and crash noise). There are no sound files.
- **Browser support:** current versions of Chrome, Edge, Firefox and Safari, on desktop and mobile.

### Project structure

```
.
├── index.html   # the entire game (HTML + CSS + JavaScript)
└── README.md    # this file
```

### Tweaking the game

The values you'll most likely want to change are near the top of the `<script>` block in `index.html`:

- `G`, `ACC`, `MAXV`, `BRAKE`, `LEAN_ACC`: gravity, acceleration, top speed, braking strength and lean strength.
- `FLIP_BONUS`: seconds taken off your time for each flip.
- `TRACKS`: each track's length, seed, hill size, jump height, stability assist and rival speeds. Add an entry here to create a new track.
- `THEMES`: sky, ground and grass colours for each setting.

---

## License

Free to use and modify. Add a license file of your choice (for example MIT) if you plan to share it publicly.
