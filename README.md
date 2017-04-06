# ReadMe: E&G Store Delivery Maps
Information about creating and editing digital delivery maps for E&G stores.
## Naming Map Files
### Map .geojson Filenames
Map .geojson files can only be renamed in GitHub by editing them. To do this 'something/anything' has to change in the code or in the filename.
### Map Description
This is actually the 'commit changes' note. This can ONLY be changed when editing the code and 'something/anything' changes.
## GeoJson.io
### Displaying Maps from GitHub
- Goto GeoJson.io and signin with your GitHub account (if you aren't already signed in).
- - You can tell if you're signed in because the upper right corner will show '[your username] | logout'.

#### Method 1: Open/Save
- In GeoJson.io goto 'Open > GitHub > erbertandgerberts > mapsdelivery > master' and click the desired map.

#### Method 2: Copy/Paste
- Goto GitHub.com and signin
- SELECT: Goto 'erbertandgerberts > mapsdelivery' and click on the desired map file.
- COPY: With the map open and visible, click the 'Raw' button. This will display the Json code. Select All and copy.
- Go back to GeoJson.io and in the right sidebar 'select all' and paste.
- The map will now show up, ready to edit.

### Displaying MULTIPLE Maps Simultaneously from GitHub
#### Method 1: Copy/Paste
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

### Converting Linestring to Polygon
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

### Adding Holes to Polygons
- The first code element in a polygon represents the exterior ring. Any subsequent code elements represent interior rings (or holes).
- For example, the following represents a square polygon with a square hole. The second code element (after the ',') is the hole.
```
{ "type": "Polygon",
    "coordinates": [
      [ [100.0, 0.0], [101.0, 0.0], [101.0, 1.0], [100.0, 1.0], [100.0, 0.0] ],
      [ [100.2, 0.2], [100.8, 0.2], [100.8, 0.8], [100.2, 0.8], [100.2, 0.2] ]
      ]
   }
```

# END of README
