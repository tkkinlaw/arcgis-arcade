# Popups using a knowledge graph

## The Arcade expression

## Arcade Experssions & Screenshots

### Map & Link Chart in ArcGIS Pro
```js
{
var query = "MATCH (:Supplier{SupplierName:$NameOfSupplier})-[:Supplies]->(:Distributor)-[:SellsTo]->(p:ProcessingPlant) RETURN p"
var plants = QueryGraph($graph, query, {'NameOfSupplier':$feature.SupplierName}) //spatial entity will behave like a $feature

var formattedCountries = ""
var countriesLayer = FeatureSetByPortalItem(Portal('https://YOUR PORTAL HERE/portal'), 'ITEMID', 0, ['COUNTRY'], True)

for (var i = 0; i < Count(plants); i++){
var plant = plants[i][0]
var plantPoint = Point({
    'x': plant['properties']['shape']["x"],
    'y': plant['properties']['shape']["y"],
    'spatialReference': plant['properties']['shape']["spatialReference"]
})

var country = Intersects(countriesLayer, plantPoint)
var plantText = plant['properties']['ProcessingPlantName'] + ": " + First(country)['COUNTRY'] + TextFormatting.NewLine
formattedCountries += plantText
}
return formattedCountries
}
```
### Knowledge Studio Link Chart

### Knowledge Studio Web Map

### Web map

### Dashboard: web map popup

### Dashboard: query results in table element

### Dashbaord: query results in pie chart element