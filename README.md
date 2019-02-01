# ReadMe: E&G Store Delivery Maps
Information about creating and editing digital delivery maps for E&G stores.
# Map Naming | Commit Titles | Comments | Colors
## Map File Naming
All maps need to be named with the following format.
- [StoreID]\_Delivery.geojson

Map files that are no longer usable should use either '\_old' or '\_bad' before the '.geojson'. If a Map File is intended for some other use (ie. showing a combination of stores), then an appropriate descriptive word should be added AFTER '\_Delivery' and before '.geojson'.

## Commit Titles
Every creation and editing of a map requires a 'Commit Title'. This title is limited to 50 characters and shows up in the map file list. In order for these titles to provide consistent, useful information, the following format should be used.
- [StoreShortName]: short description of what's changed with this 'commit' to the map. The 'what's changed' part is optional.

_Reasoning: The StoreID is already included in the map filename, the store name is helpful for those who don't have the StoreID's memorized and information about what changed is also helpful. Keep in mind the Commit Title's 50-character limit, so the 'what's changed' part might be pretty short. Note that in GitHub (as opposed to GeoJson.io) there is an ability to include a commit description with either no character limit or a very big limit._

## Comments
In order to add comments to the code (inline) to allow for searching and identifying areas in the code more easily, use the following syntax. Be sure to only change what is inside the quotes around the "Enter any comment...".
```
"_comment": "Enter any comment text in here.",
```

## Map Colors
### Color Codes
- Blue (1st): #006699 (#003366 is official E&G blue)
- Red (2nd): #9d2235
- Green (3rd): #b7bf10
### Main Delivery Area
```
"properties": {
        "stroke": "#006699",
        "stroke-width": 3,
        "stroke-opacity": 1,
        "fill": "#006699",
        "fill-opacity": 0.25
      },
```
### Store Marker
```
    {
      "type": "Feature",
      "properties": {
        "marker-color": "#006699",
        "marker-size": "medium",
        "marker-symbol": ""
      },
      "geometry": {
        "type": "Point",
        "coordinates": [
          -91.453957,
          44.749004
        ]
      }
    },
```

# Working in GeoJson.io
## ReNaming Map Files
### Map .geojson Filenames
Map .geojson files can only be renamed in GitHub by editing them. To do this 'something/anything' has to change in the code or in the filename.
### Map Description
This is actually the 'commit changes' note. This can ONLY be changed when editing the code and 'something/anything' changes.

## Editing Maps in GeoJson and Saving to GitHub
**IMPORTANT TIP**
The normal process of editing maps is...
- Goto GeoJson.io and login with your GitHub credentials.
- Goto Open > GitHub and use the arrows to find the map you're intested in and click on it.
- - Note: there is no scrollbar in this popup. To get around that (if you don't have a MacBook with trackpad), is to select some text in the map list and then use the arrow keys to move down past the visible area.
- Once the map is open, use the 'Edt Layers' tool to edit the polygon or marker.
- When the edits are complete click menu > Save and enter the commit message. BUT WAIT!
### GeoJson Edit Save Glitch
There is a bug/glitch in GeoJson.io that when you menu > Save and enter your commit message, GeoJson will error out and the menus will become unresponsive. The only way to get the menus to work again is to refresh the window, which will ERASE all of your edits. Frustrating!

To avoid this frustration, use the following procedure...
- When the edits are complete do this FIRST.
- Open the right 'code' sidebar.
- Click anywhere in the code text, Select All and COPY.
- Click menu > Save and enter the commit message. It will error out.
- Refresh the page and open the right code sidebar.
- Click anywhere in the code text, Select All and PASTE.
- NOW go menu > Save and enter the commit message. It should be successful.
- Done. With much less frustration.

## Displaying Maps from GitHub
- Goto GeoJson.io and signin with your GitHub account (if you aren't already signed in).
- - You can tell if you're signed in because the upper right corner will show '[your username] | logout'.

### Method 1: Open/Save
- In GeoJson.io goto 'Open > GitHub > erbertandgerberts > mapsdelivery > master' and click the desired map.

### Method 2: Copy/Paste
- Goto GitHub.com and signin
- SELECT: Goto 'erbertandgerberts > mapsdelivery' and click on the desired map file.
- COPY: With the map open and visible, click the 'Raw' button. This will display the Json code. Select All and copy.
- Go back to GeoJson.io and in the right sidebar 'select all' and paste.
- The map will now show up, ready to edit.

## Displaying MULTIPLE Maps Simultaneously from GitHub
### Method 1: Copy/Paste
- The only way known to do this so far is the 'copy/paste' method.
- Follow the 'Method 2: Copy/Paste' instructions above.
- Then...
- SELECT: Goto 'erbertandgerberts > mapsdelivery' and click on a DIFFERENT desired map file.
- With the map open and visible, click the 'Raw' button. This will display the Json code.
- COPY: Select All EXCEPT for the lines below and copy.
```
{
  "type": "FeatureCollection",
  "features": [
```
- Go back to GeoJson.io and in the right sidebar scroll to the bottom of the existing map code.
- Replace the following code...
```
    }
  ]
}
```
- With this...
```
    },
```
- This should tell GeoJson that there are more than one 'feature' (area) on the map and should display all of them.
- PASTE: Finally, paste the Json code AFTER the '},' code that you had replaced above.
- CONTINUE for as many maps as you need.

## Converting Linestring to Polygon
- There are three main things to change to convert a 'Linestring' map to a 'Polygon' map.
- 1: CHANGE 'Linestring' to 'Polygon' in the code below...
```
},
      "geometry": {
        "type": "Linestring", // <- Change this to 'Polygon'.
        "coordinates": [
```
- 2: ADD an extra '[' and ']' at the beginning and end of the 'geometry' code lines.
- There should be 2 at the beginning...
```
},
      "geometry": {
        "type": "Polygon",
        "coordinates": [
        [
```
- And 3 at the end...
```
[
              -91.48036479949951,
              44.80997420019494
            ]
          ]
        ]
```
- 3: VERIFY that the end coordinates are EXACTLY the same as the beginning coordinates by copy/paste the beginning coordiantes.
- That's it. If all three steps were completed correctly, the 'Linestring' should now display as a filled Polygon in GeoJson.

## Adding Holes to Polygons
- The first code element in a polygon represents the exterior ring. Any subsequent code elements represent interior rings (or holes).
- Each polygon code element begins with an enclosing '['. The second code element would start after closing ']' like this '],'.
- The comma is what separates the first enclosing '[ ]' from the second. Like this...
```
"coordinates": [
[ code element of coordinate pairs for the main polygon [1st coordinate pair], [2nd pair], [etc] ], <-closing bracket with comma
[ new code element of coordinate pairs for 'hole' polygon ]
] <-closing bracket for polygon coordinates
```
- The example below represents a square polygon with a square hole. The second code element (after the '[ ],') is the hole.
```
{ "type": "Polygon",
    "coordinates": [
      [ [100.0, 0.0], [101.0, 0.0], [101.0, 1.0], [100.0, 1.0], [100.0, 0.0] ],
      [ [100.2, 0.2], [100.8, 0.2], [100.8, 0.8], [100.2, 0.8], [100.2, 0.2] ]
      ]
   }
```
1. BEGIN by creating the main polygon.
2. THEN create the hole polygon.
3. Copy the hole polygon code element from the open enclosing bracket to the close enclosing bracket ('[ ]').
4. Paste the hole element after the main polygon code element, being sure to add the comma first.
- It can be tough to find where to insert the 'hole'. Look for the 'closing' bracket of the main polygon, add a comma and insert the hole polygon. 

# END of README
