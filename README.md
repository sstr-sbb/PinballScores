# ScoreChaser

A desktop app for tracking your standings on [ATGames ArcadeNet](https://www.atgames.net/leaderboards/titles) pinball leaderboards. Fetches the top 100 scores for all games, shows your personal rankings — even beyond the top 100 — and lets you chase higher scores.

## Features

- **ArcadeNet Login** — log in with your ArcadeNet account via browser to see your personal data
- **Personal rankings beyond top 100** — see your rank and score for all games you've played, not just the ones where you made the public leaderboard
- **All Games overview** with score thresholds for Highscore, Top 10, Top 50, and Top 100
- **Column sorting** — click any column header to sort ascending/descending
- **Hide games** — right-click to hide games you don't care about; unhide them anytime via the status bar
- **Tournament view** with drill-down into individual tournament games
- **Detail view** with full top 100 list, boxart, and color-coded ranks
- **Right-click** any player in the detail view to look up their scores
- **Parallel scraper** fetches all game titles and top 100 scores in under 20 seconds
- **Auto-refresh** on startup; data is cached locally for instant access
- **Retro LCD theme** — amber segment-display title, vivid neon accents, Share Tech Mono font

## Screenshots

![All Games overview with score thresholds](screenshots/allScores.png)

![User rankings with per-game scores and targets](screenshots/UserScore.png)

## Download

Pre-built standalone executables for Windows, Linux, and macOS are available on the [Releases](https://github.com/sstr-sbb/PinballScores/releases/latest) page. No Python installation required.

**Requirements:** Google Chrome must be installed for the ArcadeNet login feature.

**Note:** The macOS build is untested. If you run into issues, please try the source installation below.

## Installation (from source)

Requires Python 3.10+ and a working tkinter installation (included with most Python distributions).

```bash
git clone https://github.com/sstr-sbb/PinballScores.git
cd PinballScores
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Usage

```bash
source .venv/bin/activate
python app.py
```

On first launch the app will automatically fetch all leaderboard data. Subsequent launches load cached data instantly and refresh in the background.

Click **LOGIN** to sign in with your ArcadeNet account. Your personal rankings across all games will be loaded automatically. The session token is stored locally and valid for 7 days.

## How it works

The scraper uses the ATGames ArcadeNet API:

1. Game titles are fetched in parallel by prefix letter (A-Z)
2. Top 100 scores for each game are fetched concurrently (pipelined with step 1)
3. Personal rankings are fetched via authenticated API (paginated, all games)
4. Data is stored as JSON in `data/scores.json`, settings in `data/settings.json`

Login is handled via Selenium — a Chrome browser window opens for you to sign in on the ATGames website. The JWT token is extracted from localStorage after login.

The GUI is built with tkinter using a custom `ColorTable` widget that provides per-column foreground colors, click-to-sort headers, and synchronized scrolling through paired treeviews.

## AI Disclosure

This project was built with the help of [Claude Code](https://claude.ai/claude-code), an AI coding assistant by Anthropic.

## License

This project is not affiliated with ATGames. All leaderboard data is publicly available on atgames.net.

Bundled fonts: [DSEG](https://github.com/keshikan/DSEG) (OFL), [Share Tech Mono](https://fonts.google.com/specimen/Share+Tech+Mono) (OFL).
