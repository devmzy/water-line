<template>
  <div id="cesiumContainer">
    <div class="title-box">
      保护水位线查询系统
    </div>
  </div>

</template>

<script>
import * as Cesium from "cesium";

export default {
  name: "Main",
  mounted() {
    Cesium.Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI3YWEyMTRmZS0zNDI1LTQzY2ItODgyNy1jMjc4OGM2NDk2YWYiLCJpZCI6NzQ2ODcsImlhdCI6MTYzNzk3OTkxOH0.bcpqqEsuAJSOVVMs8y5FuaYl5GKUkdkN9-HPFWEo1J8';

    const viewer = new Cesium.Viewer('cesiumContainer', {
          animation: false,

          timeline: false,

          fullscreenButton: false,
          geocoder: false,
          homeButton: false,
          navigationHelpButton: false,
          sceneModePicker: false,
          baseLayerPicker: false,
          creditContainer: document.createElement("div"),

          terrainProvider: Cesium.createWorldTerrain()
        })
    ;
    let url = "http://localhost:8080/geoserver/sicau/wms"
    let parameters = {
      service: 'WMS',
      format: 'image/png',
      transparent: true,
    }

    let wstmUrl = "http://localhost:8080/geoserver/gwc/service/wmts"
    let _matrixIds = ['EPSG:4326:0', 'EPSG:4326:1', 'EPSG:4326:2', 'EPSG:4326:3', 'EPSG:4326:4', 'EPSG:4326:5', 'EPSG:4326:6', 'EPSG:4326:7', 'EPSG:4326:8', 'EPSG:4326:9', 'EPSG:4326:10',
      'EPSG:4326:11', 'EPSG:4326:12', 'EPSG:4326:13', 'EPSG:4326:14', 'EPSG:4326:15', 'EPSG:4326:16', 'EPSG:4326:17', 'EPSG:4326:18', 'EPSG:4326:19', 'EPSG:4326:20', 'EPSG:4326:21'
    ];
    let wstmPara = {
      url: wstmUrl,
      layer: "sicau:anh2", //图层名称
      style: '',
      format: 'image/png',
      tilematrixset: 'EPSG:4326',
      tileMatrixSetID: 'EPSG:4326',
      tileMatrixLabels: _matrixIds,
      tilingScheme: new Cesium.GeographicTilingScheme({
        numberOfLevelZeroTilesX: 2,
        numberOfLevelZeroTilesY: 1
      })
    }

    function wstmParameters(layer) {
      return {
        url: "http://localhost:8080/geoserver/gwc/service/wmts",
        layer: layer, //图层名称
        style: '',
        format: 'image/png',
        tilematrixset: 'EPSG:4326',
        tileMatrixSetID: 'EPSG:4326',
        tileMatrixLabels: _matrixIds,
        tilingScheme: new Cesium.GeographicTilingScheme({
          numberOfLevelZeroTilesX: 2,
          numberOfLevelZeroTilesY: 1
        })
      }

    }

    // let anh2 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:anh2"));
    // let anh3 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:anh3"));
    // let anh5 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:anh5"));
    // let anh8 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:anh8"));
    //
    // let cj2 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:cj2"));
    // let cj3 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:cj3"));
    // let cj5 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:cj5"));
    // let cj8 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:cj8"));
    //
    // let csh2 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:csh2"));
    // let csh3 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:csh3"));
    // let csh5 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:csh5"));
    // let csh8 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:csh8"));
    //
    // let ddh2 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:ddh2"));
    // let ddh3 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:ddh3"));
    // let ddh5 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:ddh5"));
    // let ddh8 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:ddh8"));
    //
    // let fj2 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:fj2"));
    // let fj3 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:fj3"));
    // let fj5 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:fj5"));
    // let fj8 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:fj8"));
    //
    // let hh2 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:hh2"));
    // let hh3 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:hh3"));
    // let hh5 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:hh5"));
    // let hh8 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:hh8"));
    //
    // let jlj2 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:jlj2"));
    // let jlj3 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:jlj3"));
    // let jlj5 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:jlj5"));
    // let jlj8 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:jlj8"));
    //
    // let lgh2 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:lgh2"));
    // let lgh3 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:lgh3"));
    // let lgh5 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:lgh5"));
    // let lgh8 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:lgh8"));
    //
    // let mj2 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:mj2"));
    // let mj3 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:mj3"));
    // let mj5 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:mj5"));
    // let mj8 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:mj8"));
    //
    // let qj2 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:qj2"));
    // let qj3 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:qj3"));
    // let qj5 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:qj5"));
    // let qj8 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:qj8"));
    //
    // let qyj2 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:qyj2"));
    // let qyj3 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:qyj3"));
    // let qyj5 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:qyj5"));
    // let qyj8 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:qyj8"));
    //
    // let tj2 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:tj2"));
    // let tj3 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:tj3"));
    // let tj5 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:tj5"));
    // let tj8 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:tj8"));
    //
    // let ylj2 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:ylj2"));
    // let ylj3 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:ylj3"));
    // let ylj5 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:ylj5"));
    // let ylj8 = new Cesium.WebMapTileServiceImageryProvider(wstmParameters("sicau:ylj8"));


    let anh2 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'anh2', parameters: parameters});
    let anh3 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'anh3', parameters: parameters});
    let anh5 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'anh5', parameters: parameters});
    let anh8 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'anh8', parameters: parameters});

    let cj2 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'cj2', parameters: parameters});
    let cj3 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'cj3', parameters: parameters});
    let cj5 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'cj5', parameters: parameters});
    let cj8 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'cj8', parameters: parameters});

    let csh2 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'csh2', parameters: parameters});
    let csh3 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'csh3', parameters: parameters});
    let csh5 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'csh5', parameters: parameters});
    let csh8 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'csh8', parameters: parameters});

    let ddh2 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'ddh2', parameters: parameters});
    let ddh3 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'ddh3', parameters: parameters});
    let ddh5 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'ddh5', parameters: parameters});
    let ddh8 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'ddh8', parameters: parameters});

    let fj2 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'fj2', parameters: parameters});
    let fj3 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'fj3', parameters: parameters});
    let fj5 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'fj5', parameters: parameters});
    let fj8 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'fj8', parameters: parameters});

    let hh2 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'hh2', parameters: parameters});
    let hh3 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'hh3', parameters: parameters});
    let hh5 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'hh5', parameters: parameters});
    let hh8 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'hh8', parameters: parameters});

    let jlj2 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'jlj2', parameters: parameters});
    let jlj3 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'jlj3', parameters: parameters});
    let jlj5 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'jlj5', parameters: parameters});
    let jlj8 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'jlj8', parameters: parameters});

    let lgh2 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'lgh2', parameters: parameters});
    let lgh3 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'lgh3', parameters: parameters});
    let lgh5 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'lgh5', parameters: parameters});
    let lgh8 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'lgh8', parameters: parameters});

    let mj2 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'mj2', parameters: parameters});
    let mj3 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'mj3', parameters: parameters});
    let mj5 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'mj5', parameters: parameters});
    let mj8 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'mj8', parameters: parameters});

    let qj2 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'qj2', parameters: parameters});
    let qj3 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'qj3', parameters: parameters});
    let qj5 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'qj5', parameters: parameters});
    let qj8 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'qj8', parameters: parameters});

    let qyj2 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'qyj2', parameters: parameters});
    let qyj3 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'qyj3', parameters: parameters});
    let qyj5 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'qyj5', parameters: parameters});
    let qyj8 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'qyj8', parameters: parameters});

    let tj2 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'tj2', parameters: parameters});
    let tj3 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'tj3', parameters: parameters});
    let tj5 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'tj5', parameters: parameters});
    let tj8 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'tj8', parameters: parameters});

    let ylj2 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'ylj2', parameters: parameters});
    let ylj3 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'ylj3', parameters: parameters});
    let ylj5 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'ylj5', parameters: parameters});
    let ylj8 = new Cesium.WebMapServiceImageryProvider({url: url, layers: 'ylj8', parameters: parameters});


    viewer.imageryLayers.addImageryProvider(anh2);
    viewer.imageryLayers.addImageryProvider(anh3);
    viewer.imageryLayers.addImageryProvider(anh5);
    viewer.imageryLayers.addImageryProvider(anh8);

    viewer.imageryLayers.addImageryProvider(cj2);
    viewer.imageryLayers.addImageryProvider(cj3);
    viewer.imageryLayers.addImageryProvider(cj5);
    viewer.imageryLayers.addImageryProvider(cj8);

    viewer.imageryLayers.addImageryProvider(csh2);
    viewer.imageryLayers.addImageryProvider(csh3);
    viewer.imageryLayers.addImageryProvider(csh5);
    viewer.imageryLayers.addImageryProvider(csh8);

    viewer.imageryLayers.addImageryProvider(ddh2);
    viewer.imageryLayers.addImageryProvider(ddh3);
    viewer.imageryLayers.addImageryProvider(ddh5);
    viewer.imageryLayers.addImageryProvider(ddh8);

    viewer.imageryLayers.addImageryProvider(fj2);
    viewer.imageryLayers.addImageryProvider(fj3);
    viewer.imageryLayers.addImageryProvider(fj5);
    viewer.imageryLayers.addImageryProvider(fj8);

    viewer.imageryLayers.addImageryProvider(hh2);
    viewer.imageryLayers.addImageryProvider(hh3);
    viewer.imageryLayers.addImageryProvider(hh5);
    viewer.imageryLayers.addImageryProvider(hh8);

    viewer.imageryLayers.addImageryProvider(jlj2);
    viewer.imageryLayers.addImageryProvider(jlj3);
    viewer.imageryLayers.addImageryProvider(jlj5);
    viewer.imageryLayers.addImageryProvider(jlj8);

    viewer.imageryLayers.addImageryProvider(lgh2);
    viewer.imageryLayers.addImageryProvider(lgh3);
    viewer.imageryLayers.addImageryProvider(lgh5);
    viewer.imageryLayers.addImageryProvider(lgh8);

    viewer.imageryLayers.addImageryProvider(mj2);
    viewer.imageryLayers.addImageryProvider(mj3);
    viewer.imageryLayers.addImageryProvider(mj5);
    viewer.imageryLayers.addImageryProvider(mj8);

    viewer.imageryLayers.addImageryProvider(qj2);
    viewer.imageryLayers.addImageryProvider(qj3);
    viewer.imageryLayers.addImageryProvider(qj5);
    viewer.imageryLayers.addImageryProvider(qj8);

    viewer.imageryLayers.addImageryProvider(qyj2);
    viewer.imageryLayers.addImageryProvider(qyj3);
    viewer.imageryLayers.addImageryProvider(qyj5);
    viewer.imageryLayers.addImageryProvider(qyj8);

    viewer.imageryLayers.addImageryProvider(tj2);
    viewer.imageryLayers.addImageryProvider(tj3);
    viewer.imageryLayers.addImageryProvider(tj5);
    viewer.imageryLayers.addImageryProvider(tj8);

    viewer.imageryLayers.addImageryProvider(ylj2);
    viewer.imageryLayers.addImageryProvider(ylj3);
    viewer.imageryLayers.addImageryProvider(ylj5);
    viewer.imageryLayers.addImageryProvider(ylj8);


    // Add Cesium OSM Buildings, a global 3D buildings layer.
    // const buildingTileset = viewer.scene.primitives.add(Cesium.createOsmBuildings());
    // Fly the camera to San Francisco at the given longitude, latitude, and height.
    viewer.camera.flyTo({
      destination: Cesium.Cartesian3.fromDegrees(103.9474447607422, 30.67519592088865, 2000000),
      orientation: {
        heading: 6.283185307179586,
        pitch: -1.5686521559334161,
      }
    });

  }
}
</script>

<style scoped>
#cesiumContainer {
  width: 100vw;
  height: 100vh;
}

.title-box {
  position: fixed;
  top: 0;
  z-index: 999;
  font-size: 48px;
  color: white;
  text-align: center;
  width: 100%
}
</style>
