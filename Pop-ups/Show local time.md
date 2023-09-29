```js
var features = FeatureSetByName($map, "World Time Zones");
var featTZ = Text(First(Intersects(features, $feature))["ZONE"]);
var tzLookup = Dictionary('{"-8":"Pacific", "-7":"Mountain", "-6":"Central", "-4":"Eastern"}');
//return tzLookup[featTZ]
var newTimestamp = DateAdd($feature.TimeStamp, Number(featTZ), 'hours');
return newTimestamp
```