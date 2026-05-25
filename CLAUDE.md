# Game Clone

## Workflow Rules
- **Never push to GitHub without explicit approval — no exceptions.** After finishing work, commit locally and stop. Wait for André to explicitly say "push it", "good to go", "send to github", etc. Context clues (e.g. needing mobile testing) are not approval.

Classic Tetris clone built as a browser game. Clean, playable, no dependencies.

## Goal
Fully functional Tetris in the browser — keyboard controls, scoring, levels, game over screen.

## Tech
- Single file: `tetris.html` — plain HTML + CSS + JavaScript
- No frameworks, no build step — just open in browser
- Audio via Web Audio API (no external files)

## Current State
**v1.4 — full mobile layout overhaul for Tetris & Dr. Mario.** Files: `index.html` (launcher), `tetris.html`, `doctor-mario.html`, `breakout.html`

**Hosted:** https://meirelesti-lab.github.io/Game-Clone/ (GitHub Pages, private repo)

### Tetris (`tetris.html`)
- 10×20 board, all 7 tetrominoes, NRS rotation (no wall kicks)
- 7-bag randomizer, immediate lock, NES scoring (capped 999,999)
- 30-level NES gravity table; level accent color cycles
- Side panel: score, level, lines, next piece preview; CRT scanline overlay
- **Level select**: `◄ LEVEL ►` on start screen (← → or 0–9); launches at chosen level
- **Mobile**: full-width canvas, board centered via ctx.translate(xOff,0); stats in side margins (SCORE/LEVEL left, LINES/NEXT right); touch bar 64px (◄ ▲ ▼ ► ▶/⏸ ♪ ⌂); ▶ starts/restarts, ♪ toggles music
- **URL param**: `?level=N` skips start screen and starts immediately
- Audio: Korobeiniki A-theme + SFX (Web Audio API, synthesized)
- Controls: `← →` move, `↑` rotate, `↓` soft drop, `P` pause, `M` music, `R`/Enter start, `ESC` menu

### Doctor Mario (`doctor-mario.html`)
- 8×16 board, Red/Yellow/Blue pills + viruses
- Match-4 any direction clears; viruses fixed, pill halves fall after clears
- **4-state rotation** (H[A,B]→V[A,B]→H[B,A]→V[B,A]→…): V→H swaps colors so left color cycles through all positions
- Wall-kick on V→H only fires at the right wall (not mid-board), preventing drift
- Chain gravity: re-checks after each clear, doubles score per chain step
- NES-style virus seeding (no 3-in-a-row placement)
- **Level select**: `◄ LEVEL ►` on start screen (← → or 0–9, max 19); `?level=N` URL param auto-starts
- **Mobile**: same full-width layout as Tetris; stats in side margins (SCORE/LEVEL left, VIRUS/NEXT right); touch bar 64px (◄ ▲ ▼ ► ▶/⏸ ♪ ⌂); ▶ starts next level on win
- Win → `N`/▶ for next level; `ESC` returns to launcher
- Audio: "Fever" theme approximation + SFX

### Breakout (`breakout.html`)
- Atari Breakout-style; full-screen canvas on mobile
- Paddle controlled by touch drag or ◄/► buttons
- Ball speeds up as bricks are cleared; multi-level brick layouts
- Touch bar: ◄ ● ► ♪ ⌂ (● = launch/pause/resume context button)

### Launcher (`index.html`)
- Three game cards with inline `◄ LEVEL ►` pickers (↑/↓ change level, ←/→ switch game)
- Launches via `game.html?level=N`; keyboard: 1/2/3/Enter/arrows; mouse hover
- CRT scanline + purple radial gradient background

### Not yet built
- High score persistence (localStorage)
- Hard drop (Space) for Tetris

## Arcade To-Do List (upcoming games)
- [ ] Frogger
- [ ] Frostbite
- [ ] Space Invaders
