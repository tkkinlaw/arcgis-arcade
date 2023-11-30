```js
<html lang="en">

<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="initial-scale=1,maximum-scale=1,user-scalable=no" />
  <title>FlowRenderer with effects and blending | Sample | ArcGIS Maps SDK for JavaScript 4.28</title>

  <link rel="stylesheet" href="https://js.arcgis.com/4.28/esri/themes/dark/main.css" />
  <script src="https://js.arcgis.com/4.28/"></script>

  <style>
    html,
    body,
    #viewDiv {
      padding: 0;
      margin: 0;
      height: 100%;
      width: 100%;
      background-color:#4c4c4c;
    }
  </style>

  <script>
   require([
      "esri/Map",
      "esri/views/MapView",
      "esri/layers/ImageryTileLayer",
      "esri/layers/TileLayer",
      "esri/layers/GroupLayer",
      "esri/rest/support/MultipartColorRamp",
      "esri/rest/support/AlgorithmicColorRamp",
      "esri/Color",
      "esri/widgets/Legend",
      "esri/widgets/Fullscreen"
    ], function (
      Map,
      MapView,
      ImageryTileLayer,
      TileLayer,
      GroupLayer,
      MultipartColorRamp,
      AlgorithmicColorRamp,
      Color,
      Legend,
      Fullscreen
    ) {
      // serves as a basemap layer
      const spilhausBasemap = new TileLayer({
        url: "https://tiles.arcgis.com/tiles/nGt4QxSblgDfeJn9/arcgis/rest/services/Spilhaus_Vibrant_Basemap/MapServer",
        effect: "saturate(10%) brightness(0.3)" // dim brightness to create darker style basemap
      });

      const colorRamp = new MultipartColorRamp({
        colorRamps: [
          new AlgorithmicColorRamp({
            fromColor: new Color([20, 100, 150, 255]),
            toColor: new Color([70, 0, 150, 255])
          }),
          new AlgorithmicColorRamp({
            fromColor: new Color([70, 0, 150, 255]),
            toColor: new Color([170, 0, 120, 255])
          }),
          new AlgorithmicColorRamp({
            fromColor: new Color([170, 0, 120, 255]),
            toColor: new Color([230, 100, 60, 255])
          }),
          new AlgorithmicColorRamp({
            fromColor: new Color([230, 100, 60, 255]),
            toColor: new Color([255, 170, 0, 255])
          }),
          new AlgorithmicColorRamp({
            fromColor: new Color([255, 170, 0, 255]),
            toColor: new Color([255, 255, 0, 255])
          }),
        ]
      });

      // sea surface temperature, visualized with raster stretch renderer
      const temperatureLayer = new ImageryTileLayer({
        url: "https://tiledimageservices.arcgis.com/jIL9msH9OI208GCb/arcgis/rest/services/HyCOM_Surface_Temperature___Spilhaus/ImageServer",
        renderer: {
          colorRamp,
          stretchType: "min-max",
          type: "raster-stretch"
        }
      });


      // ocean currents, visualized with flow renderer
      const currentsLayer = new ImageryTileLayer({
        url: "https://tiledimageservices.arcgis.com/jIL9msH9OI208GCb/arcgis/rest/services/Spilhaus_UV_ocean_currents/ImageServer",
        renderer: {
          type: "flow", // autocasts to FlowRenderer
          density: 1,
          maxPathLength: 10, // max length of a streamline will be 10
          trailWidth: "2px"
        },
        blendMode: "destination-in", // temperature layer will only display on top of this layer
      });


      const groupLayer = new GroupLayer({
        effect: "bloom(2, 0.5px, 0.0)", // apply bloom effect to make the colors pop
        layers: [temperatureLayer, currentsLayer]
      });


      const map = new Map({
        basemap: {
          baseLayers: [spilhausBasemap]
        },
        layers: [groupLayer]
      });

      const view = new MapView({
        container: "viewDiv",
        map: map,
        scale: 40000000,
        center: [-289666, -3085785]
      });
      // add legend for temperature layer
      const legend = new Legend({
        view: view,
        layerInfos: [{
          layer: temperatureLayer,
          title: "Sea surface temperature"
        }]
      });
      view.ui.add(legend, "top-right");

      // add fullscreen widget
      fullscreen = new Fullscreen({
        view: view
      });
      view.ui.add(fullscreen, "top-left");
    });
    </script>
  </head>
  <body>
    <div id="viewDiv"></div>
  </body>
</html>
```