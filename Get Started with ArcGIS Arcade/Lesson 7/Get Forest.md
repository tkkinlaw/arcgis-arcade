```js
// Return the forest polygon that intersects the selected feature 
var forestFS = FeatureSetByName($map, "Indonesian Forests", ['forest_area'])
var forest = First(Intersects($feature, forestFS))
// If the current location does intersect a feature, 
// return the forest type. Otherwise, return null.
if (!IsEmpty(forest)) {
    return forest['forest_area']
} else {
    return null
}
```