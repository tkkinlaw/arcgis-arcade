```js
var rValues = $datapoint.Rain1
var color = IIf(rValues > 20, '#0000FF', '')

return {
  //textColor:'',
  //backgroundColor:'',
  topText: $datapoint.Location,
  topTextColor: '',
  topTextOutlineColor: '',
  topTextMaxSize: 'medium',
  middleText: $datapoint.Rain1+' cm',
  middleTextColor: color,
  middleTextOutlineColor: '',
  middleTextMaxSize: 'large',
  //bottomText: '',
  //bottomTextColor: '',
  //bottomTextOutlineColor: '',
  //bottomTextMaxSize: 'medium',
  //iconName:'',
  //iconAlign:'left',
  //iconColor:'',
  //iconOutlineColor:'',
  //noValue:false,
  //attributes: {
    // attribute1: '',
    // attribute2: ''
  // }
}
```