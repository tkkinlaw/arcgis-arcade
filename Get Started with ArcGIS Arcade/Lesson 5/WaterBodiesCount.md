```js
// Count the water bodies that intersect the selected feature 
var waterBodiesFS = FeatureSetByName($map, "Water_bodies")
var int = Intersects($feature, waterBodiesFS)

// Return the water bodies count
return count(int)
```