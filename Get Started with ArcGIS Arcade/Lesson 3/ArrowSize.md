### Arrow size
This logic changes the size of the arrow according to this logic:
-If the map view's scale is less than or equal to 100,000 then the size if 30 points
-If the map view's scale is less than or equal to 500,000
```js
var vs = $view.scale
var arrowSize = when(
  vs <= 100000, 30,
  vs <= 500000, 24, 16 )
return arrowSize
```