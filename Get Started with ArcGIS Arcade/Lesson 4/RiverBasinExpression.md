```js
var fArea = Round(AreaGeodetic($feature, 'square kilometers'))
var fName = $feature.RiverBasin
var labelText = Replace(fName, "small rivers", "Unknown") + TextFormatting.NewLine + fArea

return labelText
```