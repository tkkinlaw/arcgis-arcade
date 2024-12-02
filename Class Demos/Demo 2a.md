```js
$feature.NAME + TextFormatting.NewLine + "Population: " + Text($feature.Population, '#,###')
```

**Here are various ways to write the name expression**
This one uses an unicode escape character to trigger the creation of a new line. This is built-in functionality 
```js
$feature.NAME + "\nPopulation: " + Text($feature.Population, '#,###')
```
```js
$feature.NAME + FromCharCode(10) + "Population: " + Text($feature.Population, '#,###')
```