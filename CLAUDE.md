# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains a single-file mobile children's game: **どうぶつタッチ！** (Animal Touch!), a tap-the-animal game aimed at young children on touch devices. The entire application — markup, styles, and game logic — lives in `index.html`. There is no build system, package manager, test suite, or linter.

## Running the Game

Open `index.html` directly in a browser, or serve it locally (useful for testing on a phone over LAN):

```bash
python3 -m http.server 8000
# then open http://localhost:8000/
```

There are no build or install steps.

## Architecture

Everything is in `index.html`, organized as inline `<style>` and `<script>` blocks. The script is divided into commented sections (in Japanese): 定数 (constants), 状態 (state), オーディオ (audio), ゲーム制御 (game control), スポーン (spawning), タップ (tap handling), ユーティリティ (utilities), ボタン設定 (button wiring).

Key mechanics to understand before changing gameplay:

- **Game loop**: There is no requestAnimationFrame loop. A 1-second `setInterval` (`tick`) drives the countdown timer and level, and a self-rescheduling `setTimeout` chain (`spawn`) creates animal cards. All movement is done with CSS animations (`jumpIn` keyframes), not JavaScript — cards remove themselves on `animationend`.
- **Difficulty scaling**: `level` (1–5) increases every 15 seconds of the 60-second game. Higher levels shorten the spawn interval and the card animation duration (faster animals).
- **Scoring**: Smaller cards are worth more points (`pickSize` / `sizeToPoints`: large=1, medium=3, small=5). Consecutive taps within 1.2s build a combo; combos of 3+ give a x2 multiplier, 5+ give x3.
- **Audio**: Simple beeps generated with the Web Audio API (`beep`), created lazily on first use and wrapped in try/catch so audio failures never break gameplay.
- **Persistence**: Best score is stored in `localStorage` under the key `ab2`, also wrapped in try/catch.
- **Screens**: Start and game-over screens are `.overlay` divs toggled via `style.display`; there is no routing or state machine beyond the `running` flag.

## Conventions

- The code intentionally uses conservative, widely compatible JavaScript (`var`, function declarations, no ES6+ syntax, no external dependencies) — recent commits rewrote the game specifically for reliability on older mobile browsers. Preserve this style when editing.
- All user-facing text is Japanese, written in hiragana/katakana suitable for young children (no kanji in gameplay text). Code comments are also in Japanese.
- Touch handling uses `pointerdown` (not `click`) for responsiveness, with `touch-action: manipulation` and disabled tap highlights/user selection in CSS. Keep these when adding interactive elements.
- Commit messages in this repository are written in Japanese.
