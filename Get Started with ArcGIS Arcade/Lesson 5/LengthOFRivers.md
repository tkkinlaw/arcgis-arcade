```js
// Calculate the length of rivers that intersect the selected feature 
var riversFS = FeatureSetByName($map, "Rivers")
var int = Intersects($feature, riversFS)
var riversLen = round(LengthGeodetic(int, "kilometers"))

// Return the length and add the unit of measurement 
return "Rivers Length:" + riversLen + "km"
```