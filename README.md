# FlipBook By Warp Terminal

A simple, fully client-side web application that turns any uploaded PDF into an interactive, realistic flipbook.

Created using **Warp Terminal** and its AI Agent Mode.

## Features

- Upload a PDF file directly from your browser (no backend server).
- Renders pages using [pdf.js](https://mozilla.github.io/pdf.js/) entirely in the browser.
- Two-page spread layout (like an open book).
- Realistic single-page flip animation: only the turning page moves in a 3D arc across the spine, the facing page stays static.
- Optional page-turn sound with a simple mute/unmute toggle.
- Auto-fitting layout that scales the flipbook to the available browser window space while keeping the correct aspect ratio.
- Zoom controls (zoom in, zoom out, reset to 100%).

## How it works

1. When you choose a PDF file, the app reads it into memory in the browser and passes the data to **pdf.js**.
2. pdf.js renders the PDF pages onto HTML `<canvas>` elements.
3. For each visible view, two pages are rendered side by side into a single "spread" canvas.
4. When you press **Next** or **Previous**:
   - The target spread is rendered off-screen into a buffer canvas.
   - A single "turning page" (left or right) is rendered into an overlay canvas.
   - That overlay canvas is animated using a 3D `rotateY` arc and a dynamic shadow to simulate a physical page turning across the spine.
   - Once the animation completes, the buffer spread becomes the new visible spread.
5. All logic, rendering, and animation happen in your browser; nothing is uploaded to any server.

## How to run locally

You only need a modern browser; no backend or build step is required.

### Option 1: Open directly

1. Download or clone this repository.
2. Open `index.html` in your browser (double-click or `Open with > Browser`).

> Note: Some browsers have stricter security around `file://` URLs and web workers. If you see issues with pdf.js loading, use Option 2 instead.

### Option 2: Serve with a simple local HTTP server

From the project directory (where `index.html` lives), run one of the following:

#### Using Python 3

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000/index.html
```

#### Using Node.js (npx serve)

```bash
npx serve .
```

Then open the URL printed in the terminal (usually `http://localhost:3000`).

## Usage

1. Open the app in your browser.
2. Click **Choose PDF** and select any local PDF.
3. After it loads, the header hides and the flipbook appears in the center.
4. Use **Previous** / **Next** to flip through the book.
5. Toggle **Sound: On/Off** to enable or mute the page-turn sound.
6. Use the zoom buttons to zoom out, reset to 100%, or zoom in.

## Notes

- All rendering and interaction happens client-side; your PDFs never leave your machine.
- This project was created and iterated using **Warp Terminal** and its AI Agent Mode.
