🏎️ Highway Dash
A fast-paced, browser-based lane-dodging game built with React, TypeScript, Vite, and Tailwind CSS.
---
Overview
Highway Dash is a top-down infinite runner where you control a blue car speeding down a 3-lane highway. Dodge incoming traffic, collect coins for bonus points, and survive as long as you can as the speed climbs relentlessly.
---
Gameplay
Dodge obstacles — colorful oncoming cars spawn randomly across 3 lanes.
Collect coins — golden `$` coins give +25 points each.
Survive — the game speeds up over time; one collision ends the run.
Score — accumulates continuously based on distance × speed, plus coin bonuses.
High score — saved locally in the browser between sessions.
---
Controls
Input	Action
`←` / `A`	Move left one lane
`→` / `D`	Move right one lane
`Space` / `Enter`	Start or restart
Tap left half (mobile)	Move left
Tap right half (mobile)	Move right
On-screen ◀ ▶ buttons	Move left / right (mobile)
---
Tech Stack
Tool	Version
React	19
TypeScript	5.9
Vite	7
Tailwind CSS	4
vite-plugin-singlefile	2.3
---
Project Structure
```
├── index.html
├── package.json
├── tsconfig.json
├── vite.config.ts
└── src/
    ├── main.tsx        # React entry point
    ├── App.tsx         # All game logic and rendering
    ├── index.css       # Tailwind base styles
    └── utils/
        └── cn.ts       # Tailwind class merge utility (clsx + tailwind-merge)
```
---
Getting Started
Prerequisites
Node.js 18+
npm
Install & Run
```bash
npm install
npm run dev
```
Open `http://localhost:5173` in your browser.
Build
```bash
npm run build
```
The build output (in `dist/`) is bundled into a single self-contained HTML file via `vite-plugin-singlefile` — no server required to share it.
Preview Production Build
```bash
npm run preview
```
---
Game Mechanics (Technical)
Game loop — runs via `requestAnimationFrame`; delta-time based movement for consistent speed across frame rates.
Obstacle spawning — spawn interval shortens as speed increases; at most 2 of 3 lanes can be blocked at once near the top.
Coin spawning — appears every ~1.8 s with 70% probability in a random lane.
Collision detection — AABB (axis-aligned bounding box) with a small inset margin for fairness.
Speed — starts at `5`, caps at `14`, increasing continuously by `0.00015 × dt` per frame.
High score persistence — stored in `localStorage` under the key `highway-dash-high`.
