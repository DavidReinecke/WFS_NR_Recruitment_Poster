# Flyer versions (photo layouts)

The **Flyer version** dropdown on the page is built from `manifest.json` in this folder. To add a version you only edit that file and upload your photos. The page itself does not change.

## Add a version

1. Upload your photos to `templates/images/` (JPG or PNG; roughly 1000 px or wider on the long side looks best).
2. Open `templates/manifest.json` and copy one of the existing entries inside `"templates"`. Give it a new, unique `"id"` and a `"name"` (the name is what shows in the dropdown).
3. Pick a `"layout"` and list the photos in the matching order.
4. Commit. The new version appears in the dropdown a minute or two later.

Photo file names are relative to the `templates/` folder (for example `images/elk.jpg`).

## Layouts

Photos fill the slots in this order.

| Layout | Slots (in order) |
| --- | --- |
| `standard` | 5 down the right column (top to bottom), then 4 across the bottom (left to right). **9 photos** |
| `wide-left` | 5 down the right column, then 1 wide photo across the bottom left (twice the width of a normal one), then 2 at the bottom right. **8 photos** |
| `wide-right` | 5 down the right column, then 2 at the bottom left, then 1 wide photo at the bottom right. **8 photos** |

Shapes: a right-column slot is 164 x 107.6 pt (about 1.52 : 1), a bottom slot is 136 x 107 pt (about 1.27 : 1), and a wide slot is 274 x 107 pt (about 2.56 : 1). Photos are cropped to fit their slot.

## Photo options

Each entry in `"images"` is either a file name, or an object with options:

```json
{ "src": "images/elk.jpg", "focus": [0.5, 0.35], "fit": "cover" }
```

- `focus` (optional): where to center the crop, as `[left-right, top-bottom]` from 0 to 1. The default is `[0.5, 0.5]` (the middle). Use a smaller second number to keep more of the top of a photo.
- `fit` (optional): `"cover"` (default) fills the slot and crops the edges. `"contain"` shows the whole image and fills the leftover space with `"bg"` (default white `#ffffff`). Use `contain` for maps or graphics that must not be cropped.
- `bg` (optional): background color for `contain`, for example `"#000000"`.

## Custom positions

For a layout that is not listed, give `"slots"` instead of `"layout"` and `"images"`. Positions are in points on a letter page (612 x 792, origin at the top left):

```json
{
  "id": "my-layout",
  "name": "My layout",
  "slots": [
    { "x": 417, "y": 103, "w": 164, "h": 107.6, "src": "images/elk.jpg" }
  ]
}
```

Keep photos out of the text area (left of x = 405, above y = 642) unless you also set `"bodyBottom"` on the version. `bodyBottom` is the lowest point the body text may reach (default 642).

## If something does not appear

- A version with a missing or invalid `id` or `name`, or no usable photos, is skipped.
- A photo that cannot be loaded leaves a dark box in its slot, and the page tells you.
- If `manifest.json` cannot be loaded at all, the page falls back to a built-in copy of the Classic version.
