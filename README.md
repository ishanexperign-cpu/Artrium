# Artrium library

`index.html` is the tool. Each other JSON file here is one section of its object library, and `library.json` lists them in the order they appear. Keep every file in this one folder.

**Where the page reads them from**

- On a web server, Artrium reads the JSON files directly.
- Opened from disk, browsers block pages from reading JSON files, so Artrium reads `library.js` instead. It holds the same files joined together.
- After you edit the JSON, use **Load JSON files** in the library panel and pick all the files. The page remembers them in this browser.
- To make the change permanent for anyone who opens the page from disk, click **Save library.js** and put it beside `index.html`, replacing the old one.

## An object

```json
{ "kind": "vase", "label": "Vase", "w": 0.2, "d": 0.2, "h": 0.35, "color": "#c7b8a0",
  "desc": "ceramic vase", "icon": "flower", "round": true,
  "parts": [ { "s": "lathe", "m": "ceramic", "p": [0, 0, 0], "z": [1, 1, 1],
               "pts": [[0,0],[0.32,0],[0.48,0.35],[0.22,0.86],[0.2,1]] } ] }
```

### The object

| Field | Meaning |
|---|---|
| `kind` | A unique id. |
| `w`, `d`, `h` | The default size, in metres. |
| `desc` | What the image models are told the object is. |
| `elev` | The height above the floor. |
| `wall` | When `true`, the object hugs the nearest wall when placed. |
| `seat` | When set, people can sit on it. Example: `{ "h": 0.45, "n": 2 }`. |
| `finish` | The default metal finish: `chrome`, `steel`, `black`, `gold`, `gunmetal`, `white` or `copper`. |
| `plan` | Extra lines on the plan symbol:<br>• `l`: lines<br>• `r`: rectangles<br>• `e`: ellipses<br>All in fractions of width and depth, centred on the object. |

### Parts

The front of every object faces +z, and its back is at −d/2.

| Field | Meaning |
|---|---|
| `s` (shape) | One of:<br>• `box`<br>• `rbox`: rounded corners, radius `rr` in metres<br>• `cyl`<br>• `cone`<br>• `frustum`: `top` is the top-to-bottom ratio, `seg` the number of sides<br>• `sph`<br>• `hemi`<br>• `tor`: a ring, with `tube`, `arc` and `phase`<br>• `lathe`: a profile `pts` of [radius 0–0.5, height 0–1]<br>• `flute`: a fluted panel, with `pitch` in metres |
| `m` (material) | One of: `body` (the object's colour), `fabric`, `accent`, `light`, `dark`, `black`, `white`, `wood`, `ceramic`, `metal` (the finish), `steel`, `gold`, `glass`, `frost`, `mirror`, `screen`, `shadow`, `green`, `terra`, `top` (kitchen countertop), `kfront`, `kcarc`, or a hex colour such as `#3e6e8e`. |
| `p` (position) | `[x, y, z]`: the centre in x and z, the bottom in y. For `tor`, the centre of the ring. |
| `z` (size) | `[sx, sy, sz]`. |
| `r` (rotation) | `[rx, ry, rz]` in degrees, turning about the part's bottom centre. |

**Numbers and expressions**

- A number is a fraction of the object's width (x), height (y) or depth (z), so the part scales when the object is resized.
- A string is an expression in metres. It can use `w`, `d`, `h`, `+ - * /`, brackets, `min()`, `max()` and `abs()`. For example, `"d/2-0.02"` keeps a part 2 cm in from the front at any depth.

### Kitchen units

Kitchen units use `"builder": "kunit"` with `params`:

| Param | Values |
|---|---|
| `unit` | `base`, `wall` or `tall` |
| `fronts` | `doors`, `drawers`, `mixed`, `open`, `flap`, `corner` or `appliance` |
| `doors` | number |
| `drawers` | number |
| `pots` | `true` or `false` |
| `overhang` | metres |

Shutters, handles and the countertop come from the kitchen panel in the page.
