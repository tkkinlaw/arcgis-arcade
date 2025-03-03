Use with the Indonesian Forests web map in ArcGIS Pro. This uses the Text formatting tags to modify label color.
Information can be found here: https://pro.arcgis.com/en/pro-app/latest/help/mapping/text/text-formatting-tags.htm
```js
var a = $feature.Area;

if (a > 5) {
return $feature.forest_are + Textformatting.NewLine + "<CLR cyan = '38' magenta = '100' yellow = '100' black = '0'>" + 'Area: ' + text(a, "#,###") + " km²" + "</CLR>"
} else {
  return "";
}
```
Single color:
```js
var a = $feature.Area;

if (a > 5) {
return $feature.forest_are + Textformatting.NewLine + "<CLR blue = '255'>" + 'Area: ' + text(a, "#,###") + " km²" + "</CLR>"
} else {
  return "";
}
```
