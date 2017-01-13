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
- Goto 'erbertandgerberts > mapsdelivery' and click on the desired map file.
- With the map open and visible, click the 'Raw' button. This will display the Json code. Select All and copy.
- Go back to GeoJson.io and in the right sidebar 'select all' and paste.
- The map will now show up, ready to edit.
### Displaying MULTIPLE Maps Simultaneously from GitHub
#### Method 1: Copy/Paste
- The only way known to do this so far is the 'copy/paste' method.
- Follow the 'Method 2: Copy/Paste' instructions above.
- Then...
- Goto 'erbertandgerberts > mapsdelivery' and click on a DIFFERENT desired map file.
- With the map open and visible, click the 'Raw' button. This will display the Json code.
- Select All EXCEPT for the lines below and copy.
    {
      "type": "FeatureCollection",
      "features": [
- Go back to GeoJson.io and in the right sidebar scroll to the bottom of the existing map code.
- Replace the following code...
        }
      ]
    }
- With this...
        },
- This should tell GeoJson that there are more than one 'feature' (area) on the map and should display all of them.
- CONTINUE for as many maps as you need.
# END of README
