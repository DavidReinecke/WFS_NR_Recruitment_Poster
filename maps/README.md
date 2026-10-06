# Geographic area maps

Each geographic area can have one map picture. It is drawn at the top of the "About the Unit" page(s), above the unit writeups, whenever a flyer selects a unit that has a writeup.

## Add or change a map

1. Upload the picture to this `maps/` folder (JPG or PNG, about 1700 px wide works well; crop off any title and footer so only the map shows).
2. Open the page, choose **Edit areas, units & writeups** (library admin), pick the area, and type the file path in **Map picture file**, for example `maps/alaska.jpg`.
3. Choose **Publish changes**.

Or edit `units.json` directly and add `"map": "maps/alaska.jpg"` to the area. An area with no map (or a file that cannot be loaded) simply shows the writeups without a picture.
