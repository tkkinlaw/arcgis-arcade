```js
// Assign variables
var rTotal = 0
var rFall1 = $feature.Rain1
var rFall2 = $feature.Rain2
var rFall3 = $feature.Rain3

// Sum values that are greater than or equal to 2.5
if (rFall1 >= 2.5){
rTotal += rFall1
};

if (rFall2 >= 2.5){
rTotal += rFall2
};

if (rFall3 >= 2.5){
rTotal += rFall3
};

// Return the average of the three values and round the number to one decimal place
return round(rTotal/3,1)
```