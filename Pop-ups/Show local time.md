This script works with point data with a time stamp. Points may be scattered across time zones. This script displays the time of collection in the local ime zone in the pop-up. 
```js
var features = FeatureSetByName($map, "World Time Zones");
var featTZ = Text(First(Intersects(features, $feature))["ZONE"]);
var tzLookup = Dictionary('{"-8":"Pacific", "-7":"Mountain", "-6":"Central", "-4":"Eastern"}');
var newTimestamp = DateAdd($feature.TimeStamp, Number(featTZ), 'hours');
return newTimestamp
```