# Fruit Drop AI 🍓

A browser-based fruit-dropping physics game with a built-in Genetic Algorithm that learns to play — entirely in vanilla HTML/CSS/JS, no build tools required.

![demo](https://img.shields.io/badge/play-open%20index.html-brightgreen)

## What it is

Drop fruits into a box. When two identical fruits touch, they merge into the next larger fruit. Stack high enough and it's game over. Simple rules, surprisingly deep strategy.

What makes this project different: **the game trains itself**. A Genetic Algorithm runs hundreds of simulated games headlessly, evolves a genome of evaluation weights, and produces an AI that plays better each generation. A 4×4 live grid lets you watch all 16 individuals of the current generation compete simultaneously.

## Features

- **12 fruit types** — from tiny salmon roe (いくら) up through cherry, strawberry, and beyond, each with distinct physics properties
- **Matter.js physics** — real rigid-body simulation with tunneling prevention (120 px thick walls, high solver iterations)
- **AI auto-play** — press `A` to toggle; the AI evaluates every candidate drop position using a genome-weighted heuristic
- **Genetic Algorithm trainer** — evolves 5 genome weights (merge bonus · stack height · danger zone · edge penalty · center bias) across unlimited generations
- **MAP-Elites archive** — instead of tracking a single best genome, maintains a 4×4 behavioral map keyed by (drop-position preference × merge rate); each cell holds the champion for that play style
- **Live visualizations** — single-game 8× preview or a 4×4 multi-game grid showing the whole population in real time
- **Kirby** — a pink character that walks, charges, and jumps around inside the box; toggle on/off so it doesn't interfere with training

## How to play

```bash
# No installation needed — just open the file
open index.html
```

| Control | Action |
|---------|--------|
| Mouse move | Aim the drop position |
| Click / Space | Drop fruit |
| `A` | Toggle AI auto-play |

The GA panel is at the bottom of the page. Hit **▶ 学習開始** to start training, **✓ AIに適用** to apply the best genome found so far to the live game.

## How the GA works

```
Population (16 genomes)
    │
    ▼
Simulate each genome as a full headless game (Matter.js, no render)
    │  records: score · avg drop x · merge rate
    ▼
Update MAP-Elites archive (4×4 grid keyed on behavior)
    │
    ▼
Select top-4 elites + crossover offspring + 4 archive injections
    │
    ▼
Next generation (repeat)
```

Genomes are saved to `localStorage` — progress survives page reloads.

## Tech stack

| Layer | Technology |
|-------|-----------|
| Physics | [Matter.js](https://brm.io/matter-js/) v0.19.0 (CDN) |
| Rendering | Canvas 2D API |
| AI / GA | Vanilla JS (no ML libraries) |
| Styles | Plain CSS, dark theme |
| Bundler | None — single `index.html` |

## Project structure

```
index.html   ← entire game: HTML + CSS + JS in one file (~1600 lines)
README.md
```

## License

MIT
