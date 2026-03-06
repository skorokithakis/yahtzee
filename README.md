# Yahtzee Scorecard

A real-time, multiplayer Yahtzee scorecard web app. Open it on two phones, enter
the same room code, and your scores sync instantly -- no app install, no account,
no backend to run.

This is **not** a Yahtzee game engine. It's a digital scorecard you use alongside
physical dice. Two players share a room and see each other's score updates in
real time.

## Features

- **Room-based multiplayer** -- join the same 5-character room code to share a
  scorecard.
- **Full Yahtzee scorecard** -- upper section (Ones through Sixes with bonus
  calculation), lower section (Three/Four of a Kind, Full House, straights,
  Yahtzee, Chance), Yahtzee bonus slots, and auto-calculated totals.
- **Real-time sync** -- scores update on both screens within milliseconds, powered
  by [Gweet](https://gweet.stavros.io).
- **Screen wake lock** -- keeps your phone screen on while you play.
- **Mobile-first** -- compact layout designed for phones, with numeric keyboards
  and large touch targets.
- **Zero dependencies** -- the entire app is a single HTML file with no
  frameworks, no build step, and no package manager.

## Usage

Open `index.html` in a browser. That's it.

To serve it locally:

```bash
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.

On both devices, enter the same room code and start scoring. An internet
connection is required for sync (the app talks to `gweet.stavros.io`).

## How It Works

The app is a single `index.html` file containing all HTML, CSS, and JavaScript.
State synchronization between players uses [Gweet](https://gweet.stavros.io), a
lightweight real-time messaging service:

- When a player joins a room, the latest state is fetched.
- A streaming connection stays open for live updates.
- On any input change, the full scorecard state is sent (debounced at 300ms).
- Self-echo suppression prevents feedback loops.

There is no custom backend -- Gweet handles all the real-time plumbing.

## License

This project is licensed under the [GNU Affero General Public License v3.0](LICENSE).
