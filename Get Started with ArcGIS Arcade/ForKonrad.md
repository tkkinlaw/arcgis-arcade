
Python code to generate a list of layers from an ArcGIS Pro map.

```py
aprx = arcpy.mp.ArcGISProject("Current")
layerList = []
for lyr in aprx.activeMap.listLayers():
    layerList.append(lyr.name)
print(layerList)
```

Arcade code to search for the FacilityID field across a list of layers and return that value.
```js
var layerNameArray = [
  "LANDUSE_FINAL10_12",
  "KEN_PowerPlants",
  "PowerPoles",
  "GDB_ValidationPointErrors",
  "GDB_ValidationLineErrors",
  "GDB_ValidationPolygonErrors"
];

var facilityIDArray = [];
// all layers have a common FacilityID (this unique ID can be replaced)
for (var index in layerNameArray) {
  if (Count(facilityIDArray) == 0) {
    var fs = FeatureSetByName(
      $map,
      layerNameArray[index],
      ["FacilityID"],
      True
    );
    var int = First(Intersects(fs, $feature));
    Insert(facilityIDArray, Count(facilityIDArray), int["FacilityID"]);
  } else {
    break; // stop iterating any futher
  }
}

// At this point, facilityIDArray is an Array of strings derived from the list of layers' FacilityID field. 
// Because of the if statement, it can only contain one value.

// Input point layer also has the SiteID, FacilityID, RPUID - in the form, we just process one ID at a time
return facilityIDArray[0]
```