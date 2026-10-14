# Memory Blocks Game

A browser-based card-matching memory game built with vanilla HTML, CSS and JavaScript, featuring 3D flip animations, shuffled tiles and sound feedback.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6-F7DF1E?logo=javascript&logoColor=black)
![No Dependencies](https://img.shields.io/badge/dependencies-none-brightgreen)

---

## Overview

**Memory Blocks Game** is a classic "concentration" style game: the board contains 20 face-down blocks forming 10 pairs of technology logos (Angular, Vue.js, CSS3, GitHub, Gulp.js, HTML5, Jest, MongoDB, Python and React). The player flips two blocks at a time and tries to find every matching pair while making as few wrong guesses as possible.

The project is a front-end practice exercise that demonstrates core web fundamentals without any framework or build tooling:

- DOM selection and event handling
- Array shuffling (Fisher–Yates algorithm) combined with the CSS Flexbox `order` property
- 3D CSS transforms (`rotateY`, `transform-style: preserve-3d`, `backface-visibility`)
- Using `data-*` attributes to compare elements
- Playing audio through the HTML `<audio>` element

## Features

- **Start screen** – a full-screen overlay with a "Start Game" button; clicking it prompts for the player's name.
- **Player greeting** – the entered name is shown in the info bar (`Hello: <name>`); an empty or cancelled prompt falls back to `Unknown`.
- **Random layout on every load** – block positions are shuffled with a Fisher–Yates shuffle and applied through the Flexbox `order` property, so the HTML stays static while the visual order changes.
- **3D flip animation** – each block has a front face (a "!" placeholder) and a back face (the logo) that rotate in 3D on click.
- **Match detection** – when two blocks are flipped, their `data-technology` attributes are compared:
  - **Match:** both blocks stay revealed (`has-match`) and a success sound plays.
  - **Mismatch:** the "Wrong Tries" counter increases, a fail sound plays, and both blocks flip back after 1 second.
- **Click lock** – while two blocks are being evaluated, the board is temporarily disabled (`pointer-events: none`) for the effect duration to prevent extra clicks.
- **Wrong tries counter** – tracks the number of failed attempts as a simple score.

## Tech Stack

| Layer      | Technology                                                       |
| ---------- | ---------------------------------------------------------------- |
| Markup     | HTML5 (`<audio>` elements, `data-*` attributes)                  |
| Styling    | CSS3 (Flexbox, 3D transforms, transitions)                       |
| Logic      | Vanilla JavaScript (ES6: `let`, arrow functions, `Array.from`)   |
| Assets     | PNG logos and MP3 sound effects                                  |

No frameworks, libraries, package managers or build steps are required.

## Project Structure

```
Memory-Blocks-Game/
├── README.md
└── Memory Blocks Game/
    ├── MemoryBlocksGame.html   # Page markup: start overlay, info bar, 20 game blocks, audio tags
    ├── MemoryBlocksGame.css    # Layout, overlay, info bar and 3D flip styles
    ├── MemoryBlocksGame.js     # Game logic: start/name prompt, shuffle, flip, match check
    ├── imgs/                   # Technology logos used on the back of the blocks (10 PNGs)
    └── Sound/
        ├── success.mp3         # Played when a pair is matched
        └── fail.mp3            # Played on a wrong guess
```

## Getting Started

### Prerequisites

- Any modern web browser (Chrome, Firefox, Edge, Safari).
- Optional: a local static server such as the VS Code **Live Server** extension.

### Installation

```bash
git clone https://github.com/hamdiwerhanii/Memory-Blocks-Game.git
cd Memory-Blocks-Game
```

### Running the game

**Option 1 – open the file directly**

Open [`Memory Blocks Game/MemoryBlocksGame.html`](Memory%20Blocks%20Game/MemoryBlocksGame.html) in your browser.

**Option 2 – use a static server (recommended)**

Some browsers restrict audio playback for local files. Serving the folder avoids this:

```bash
# Using VS Code: right-click MemoryBlocksGame.html → "Open with Live Server"

# Or with Python 3
cd "Memory Blocks Game"
python -m http.server 8000
# then visit http://localhost:8000/MemoryBlocksGame.html

# Or with Node.js
npx serve "Memory Blocks Game"
```

## How to Play

1. Click **Start Game** and enter your name (or leave it empty to play as "Unknown").
2. Click a block to flip it and reveal its logo.
3. Click a second block:
   - If both logos match, they stay face up.
   - If they don't, your **Wrong Tries** count goes up and both blocks flip back after one second.
4. Keep going until all 10 pairs are revealed — try to finish with the lowest number of wrong tries.

## How It Works

| Function / Step                 | Responsibility                                                                                     |
| ------------------------------- | -------------------------------------------------------------------------------------------------- |
| Start button `onclick`          | Prompts for the player's name, writes it to the info bar and removes the start overlay.            |
| `shuffle(array)`                | Fisher–Yates shuffle of the index array `[0 … 19]`.                                                |
| Block initialisation            | Assigns each block a shuffled `style.order` value and attaches a click listener.                   |
| `flipBlock(block)`              | Adds `is-flipped`; when two blocks are flipped, locks the board and checks for a match.            |
| `stopClicking()`                | Adds `no-clicking` to the board container and removes it after `duration` (1000 ms).               |
| `checkMatchedBlocks(a, b)`      | Compares `data-technology`; marks matches with `has-match` or increments the wrong-tries counter.  |

To add or swap a pair, duplicate a `.game-block` element in the HTML with the same `data-technology` value and a new image in `imgs/`. The shuffle automatically adapts to the number of blocks.

## Project Status & Roadmap

The game is playable, but it is a learning project with some known limitations:

- **No end-of-game state** – nothing happens when all pairs are found (no win message, timer or final score).
- **No restart button** – the page must be reloaded to play again.
- **Fixed-width layout** – the board and info bar use fixed widths (1100px / 1080px), so the game is not responsive on smaller screens.
- **Accessibility** – logo images have empty `alt` attributes and blocks are not keyboard-operable.

Possible improvements:

- [ ] Win screen showing the player's name and number of wrong tries
- [ ] "Play again" button that reshuffles without reloading
- [ ] Timer and best-score persistence (e.g. `localStorage`)
- [ ] Responsive grid for tablets and mobile devices
- [ ] Difficulty levels (number of pairs) and generating blocks from a JavaScript data array instead of hard-coded HTML
- [ ] Keyboard support and descriptive `alt` text

## Contributing

Contributions, suggestions and bug reports are welcome. Fork the repository, create a feature branch, commit your changes and open a pull request.

## License

No license file is currently included; all rights reserved by the author.

## Author

**Hamdi Werhani** — GitHub [@hamdiwerhanii](https://github.com/hamdiwerhanii)
