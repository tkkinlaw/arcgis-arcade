```js
var fArea = $feature["Area"]

if(fArea > 1){
  return round(fArea,0) + " km²";
} else {
  return "";
}
```

To get thousands seperators, replace the Round functionwith the text function:
```js
var a = $feature.Area;

if (a > 1) {
  return text(a, "#,###") + " km²";
} else {
  return "";
}
```