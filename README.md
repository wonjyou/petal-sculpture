# Interactive Petal Sculpture

An interactive 3D sculpture inspired by the petal sculpture at Singapore Changi Airport, the Petalclouds kinetic installation in Terminal 4. Eighteen polished metal rings, each shaped like a rounded triangle, hang in the air like a crib mobile. You can brush them with the cursor to set them twirling, switch between five arrangements and four metals, and move the camera around the piece.

It runs in the browser from a single HTML file. There is no build step and nothing to install.

## Running it

Open `index.html` in a browser. You can also serve the folder over HTTP:

```bash
python3 -m http.server 5183
```

Then visit http://localhost:5183.

The page loads three.js from a CDN, so it needs an internet connection the first time. It needs WebGL2, which current Chrome, Edge, Firefox and Safari all support.

## Controls

The configuration switch, the metal swatches and the orbit button sit in a row at the bottom of the page. The help button is in the top right corner.

| Input | What it does |
| --- | --- |
| Move the cursor across the rings | Spins each ring you pass over in the direction of travel and nudges it aside. Faster strokes spin harder |
| Click or tap a ring | Gives it a sharper flick |
| Configuration buttons or keys `1` to `5` | Switch between Vortex, Clouds, Wings, Bloom and Drift |
| Colour swatches or `M` | Change the metal: silver, gold, rose gold or bronze. `M` steps through them in that order |
| Orbit button or `O` | Turn the slow automatic orbit on or off |
| Click and drag | Rotate the view around the sculpture. Horizontal drag has no limit; vertical drag stops at about 70 degrees above or below level |
| Scroll wheel, trackpad pinch, or the up and down arrow keys | Zoom in and out |
| Double-click | Return to the front, level view at the starting distance |
| Help button or `?` | Open a panel listing these controls. `Esc`, the close button, or a click outside the panel closes it |

Hovering over a swatch or the orbit button shows a small label with its name.

The orbit button shows a planet with a moon. While orbit is on, the moon circles the planet. The automatic orbit pauses while you drag and carries on from wherever you leave the view. With orbit off, the view stays where you put it.

While the help panel is open, the sculpture ignores the keyboard shortcuts and the scroll wheel.

On a touch screen, dragging a finger brushes the rings. Rotating the view by dragging is for the mouse.

## How the rings behave

Each ring hangs from its own invisible vertical thread and is loosely tied to its neighbours. When you set one turning, the thread twists and pulls it back, and the neighbours are dragged round after it. The twirl runs down the line as a wave, swings back, and settles over about ten seconds.

Left alone, the mobile still moves. Every five to ten seconds a breath of air catches one ring at random and starts a small cascade.

## The configurations

All five use the same eighteen rings. Each configuration is a set of numbers for size, spacing, twist and motion, and switching eases every number toward its new value, so the rings glide from one arrangement into the next. The page opens on Vortex.

Vortex nests the rings one inside the next and points them away from the camera, so you look down a twisting tunnel. It swirls steadily while the twist deepens and relaxes.

Clouds follows the Petalclouds form: equal rings spaced along a diagonal axis, each turned a little further round than the last. The helix slowly winds tight and unwinds.

Wings hinges two fans of nested rings on a vertical spine. The fans beat open and shut, and the whole piece turns to show them.

Bloom hangs each ring by one corner around a short stem, like a flower facing the viewer. It opens and closes its petals and rotates slowly.

Drift strings the rings loosely down a diagonal. Each one bobs and turns in its own time, and the rear rings dim toward the background.

## The surface

The rings are fully metallic with a low roughness, so almost everything you see on them is reflection. The scene reflects a dark studio with a few bright softboxes, which is what makes the surface read as polished metal. Three slow lights travel with the camera and sweep highlights along the bands. A small amount of bloom is applied; set `GLOW` to `0` to remove it.

Each ring is a solid band: a flat bar about a third as thick as it is wide, with a bevel on all four edges. The bevels catch their own highlights.

The page opens in silver. The swatches change the colour and roughness of the metal, and the change eases in over about a second.

## Tuning

The constants at the top of the script in `index.html` control the feel of the piece.

| Constant | What it sets |
| --- | --- |
| `RINGS` | Number of rings |
| `TEMPO` | Overall speed of the idle motion |
| `GLOW` | Bloom strength |
| `ORBIT_SPEED` | How fast the automatic orbit circles |
| `CAMERA_Z` | Starting camera distance |
| `ZOOM_NEAR`, `ZOOM_FAR` | Closest and furthest camera distance |
| `PITCH_LIMIT` | How far a drag can tip the camera |
| `MORPH` | How quickly one configuration eases into the next |
| `TWIST_BACK` | How firmly a ring's thread turns it back to rest |
| `TWIST_PASS` | How strongly a twirl spreads to neighbouring rings |
| `TWIST_DRAG` | How quickly a twirl dies away |
| `SWING_BACK`, `SWING_PASS`, `SWING_DRAG` | The same three settings for the sideways sway |
| `TWIRL`, `PUSH` | How hard the cursor spins and shoves a ring |

To add a configuration, copy one of the entries in `CONFIGS`, change its numbers, and add a button with a matching `data-config` name. The comment above `CONFIGS` explains each number. The number keys follow the order of the buttons.

To add a metal, add an entry to `MATERIALS` with a colour and a roughness, and add a swatch button with a matching `data-material` name.

The shape of the ring outline is set by `CORNER`: `0` is a circle, and higher values pull it toward a triangle. The band's cross-section is defined in `FACES`, where `B` is its thickness and `C` is the size of the bevel.
