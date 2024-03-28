```js
// Fetches features from the Indonesia Substations web layer
var pFeatureSet = FeatureSetByPortalItem(
  Portal('https://www.arcgis.com'),
  'c5507bca5a2a4da68db0c699e8b70e19',
  0,
  ["*"],
  false
);

return pFeatureSet
```

Return an integer of how many features there are in the feature set
```js
return COUNT(pFeatureSet)
```

Return a subset of the features in the feature set
```js
return Filter(pFeatureSet, 'kV > 150')
```