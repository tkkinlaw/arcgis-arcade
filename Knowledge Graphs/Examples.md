# Arcade Experssions using Knowledge Graphs

## Pop up expression
```js
var query = 'MATCH (:Supplier{SupplierName:$NameOfSupplier})-[:Supplies]->(:Distributor)-[:SellsTo]->(p:ProcessingPlant) RETURN p'
var plants = QueryGraph($graph, query, {'NameOfSupplier':$feature.SupplierName})

var formattedCountries = ''
var p = Portal('https://YOUR PORTAL HERE/portal')
var itemID = 'ItemID12345'
var countriesLayer = FeatureSetByPortalItem(p, itemID, 0, ['COUNTRY'], True)

for (var i = 0; i < Count(plants); i++){
var plant = plants[i][0]
var plantPoint = Point({
    'x': plant['properties']['shape']['x'],
    'y': plant['properties']['shape']['y'],
    'spatialReference': plant['properties']['shape']['spatialReference']
})

var country = Intersects(countriesLayer, plantPoint)
var plantText = plant['properties']['ProcessingPlantName'] + ': ' + First(country)['COUNTRY'] + TextFormatting.NewLine
formattedCountries += plantText
}
return formattedCountries
```
## Dashboard expressions
### Table element
```js
var p = Portal('https://YOUR PORTAL HERE/portal')
var itemID = 'ItemID12345'
var kg = KnowledgeGraphByPortalItem(p, itemID);
var query = 'MATCH ()-[r:SellsTo]-(p:ProcessingPlant) WITH p, COUNT(r) as rNum RETURN p.ProcessingPlantName, rNum';
var results = QueryGraph(kg, query);
var featList = [];

for (var i in results) {Push(featList,
    { attributes: { PlantName: results[i][0], Count: results[i][1] } })}

var jsonDictionary = { fields: [
    { alias: 'Plant Name', name: 'PlantName', type: 'esriFieldTypeString' },
    { alias: 'Count', name: 'Count', type: 'esriFieldTypeInteger' }
  ],
  spatialReference: { wkid: 4326 },
  geometryType: 'esriGeometryPoint',
  features: featList};

return FeatureSet(Text(jsonDictionary));
```

### Pie chart element
```js
var p = Portal('https://YOUR PORTAL HERE/portal')
var itemID = 'ItemID12345'
var kg = KnowledgeGraphByPortalItem(p, itemID);
var query = 'MATCH (s:Supplier)-[]-()-[:SellsTo]-(p:ProcessingPlant) RETURN s.Material, p.ProcessingPlantName';
var results = QueryGraph(kg, query);
var FeatList = [];

for (var i in results) {Push(FeatList,
    { attributes: { SupplierMaterial: results[i][0], PlantName: results[i][1]} })}

var jsonDictionary = { fields: [
    { alias: 'Supplier Material', name: 'SupplierMaterial', type: 'esriFieldTypeString' },
    { alias: 'Plant Name', name: 'PlantName', type: 'esriFieldTypeString' }
  ],
  spatialReference: { wkid: 4326 },
  geometryType: 'esriGeometryPoint',
  features: featList};

return FeatureSet(Text(jsonDictionary));
```