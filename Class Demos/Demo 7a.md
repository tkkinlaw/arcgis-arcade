## Get Date - form calculation - Date field
```js
Now()
```
## Get User Info - form calculation - user name
```js
var userInfo = GetUser(Portal('https://kinlaw.maps.arcgis.com/'))
return userInfo['fullName']
```