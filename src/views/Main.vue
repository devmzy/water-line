<template>
  <div id="cesiumContainer">
    <div class="title-box">
      保护水位线查询系统
    </div>
    <div class="layer-select-box">
      <el-checkbox @change="checked => changeRiverLayer(checked,item.label)" v-for="item in riverLayerList"
                   :label="item.name"
                   size="large"/>
      <el-checkbox @change="checked => changeOtherLayer(checked,item.label)" v-for="item in otherLayerList"
                   :label="item.name"
                   size="large"/>
    </div>
    <div class="area-select-box">
      <el-cascader
          v-model="value"
          :options="options"
          :props="props"
          @change="areaChange"
      />
    </div>
  </div>

</template>

<script>
import * as Cesium from "cesium";

export default {
  name: "Main",
  data() {
    return {
      riverLayerList: [
        {
          "name": "安宁河",
          "label": "anh"
        },
        {
          "name": "赤水河",
          "label": "csh"
        },
        {
          "name": "大渡河",
          "label": "ddh"
        },
        {
          "name": "涪江",
          "label": "fj"
        },
        {
          "name": "黄河",
          "label": "hl"
        },
        {
          "name": "嘉陵江",
          "label": "jlj"
        },
        {
          "name": "泸沽湖",
          "label": "lgh"
        },
        {
          "name": "岷江",
          "label": "mj"
        },
        {
          "name": "青衣江",
          "label": "qyj"
        },
        {
          "name": "渠江",
          "label": "qj"
        },
        {
          "name": "沱江",
          "label": "tj"
        },
        {
          "name": "雅砻江",
          "label": "ylj"
        },
        {
          "name": "长江（金沙江）",
          "label": "cj"
        },

      ],
      otherLayerList: [
        {
          "name": "行政区划",
          "label": "xzqh"
        },
        {
          "name": "流域",
          "label": "ly"
        }
      ],
      value: "",
      options: [
        {
          value: 'guide',
          label: 'Guide',
          children: [
            {
              value: 'disciplines',
              label: 'Disciplines',
              children: [
                {
                  value: 'consistency',
                  label: 'Consistency',
                },
                {
                  value: 'feedback',
                  label: 'Feedback',
                },
                {
                  value: 'efficiency',
                  label: 'Efficiency',
                },
                {
                  value: 'controllability',
                  label: 'Controllability',
                },
              ],
            },
            {
              value: 'navigation',
              label: 'Navigation',
              children: [
                {
                  value: 'side nav',
                  label: 'Side Navigation',
                },
                {
                  value: 'top nav',
                  label: 'Top Navigation',
                },
              ],
            },
          ],
        },
        {
          value: 'component',
          label: 'Component',
          children: [
            {
              value: 'basic',
              label: 'Basic',
              children: [
                {
                  value: 'layout',
                  label: 'Layout',
                },
                {
                  value: 'color',
                  label: 'Color',
                },
                {
                  value: 'typography',
                  label: 'Typography',
                },
                {
                  value: 'icon',
                  label: 'Icon',
                },
                {
                  value: 'button',
                  label: 'Button',
                },
              ],
            },
            {
              value: 'form',
              label: 'Form',
              children: [
                {
                  value: 'radio',
                  label: 'Radio',
                },
                {
                  value: 'checkbox',
                  label: 'Checkbox',
                },
                {
                  value: 'input',
                  label: 'Input',
                },
                {
                  value: 'input-number',
                  label: 'InputNumber',
                },
                {
                  value: 'select',
                  label: 'Select',
                },
                {
                  value: 'cascader',
                  label: 'Cascader',
                },
                {
                  value: 'switch',
                  label: 'Switch',
                },
                {
                  value: 'slider',
                  label: 'Slider',
                },
                {
                  value: 'time-picker',
                  label: 'TimePicker',
                },
                {
                  value: 'date-picker',
                  label: 'DatePicker',
                },
                {
                  value: 'datetime-picker',
                  label: 'DateTimePicker',
                },
                {
                  value: 'upload',
                  label: 'Upload',
                },
                {
                  value: 'rate',
                  label: 'Rate',
                },
                {
                  value: 'form',
                  label: 'Form',
                },
              ],
            },
            {
              value: 'data',
              label: 'Data',
              children: [
                {
                  value: 'table',
                  label: 'Table',
                },
                {
                  value: 'tag',
                  label: 'Tag',
                },
                {
                  value: 'progress',
                  label: 'Progress',
                },
                {
                  value: 'tree',
                  label: 'Tree',
                },
                {
                  value: 'pagination',
                  label: 'Pagination',
                },
                {
                  value: 'badge',
                  label: 'Badge',
                },
              ],
            },
            {
              value: 'notice',
              label: 'Notice',
              children: [
                {
                  value: 'alert',
                  label: 'Alert',
                },
                {
                  value: 'loading',
                  label: 'Loading',
                },
                {
                  value: 'message',
                  label: 'Message',
                },
                {
                  value: 'message-box',
                  label: 'MessageBox',
                },
                {
                  value: 'notification',
                  label: 'Notification',
                },
              ],
            },
            {
              value: 'navigation',
              label: 'Navigation',
              children: [
                {
                  value: 'menu',
                  label: 'Menu',
                },
                {
                  value: 'tabs',
                  label: 'Tabs',
                },
                {
                  value: 'breadcrumb',
                  label: 'Breadcrumb',
                },
                {
                  value: 'dropdown',
                  label: 'Dropdown',
                },
                {
                  value: 'steps',
                  label: 'Steps',
                },
              ],
            },
            {
              value: 'others',
              label: 'Others',
              children: [
                {
                  value: 'dialog',
                  label: 'Dialog',
                },
                {
                  value: 'tooltip',
                  label: 'Tooltip',
                },
                {
                  value: 'popover',
                  label: 'Popover',
                },
                {
                  value: 'card',
                  label: 'Card',
                },
                {
                  value: 'carousel',
                  label: 'Carousel',
                },
                {
                  value: 'collapse',
                  label: 'Collapse',
                },
              ],
            },
          ],
        },
        {
          value: 'resource',
          label: 'Resource',
          children: [
            {
              value: 'axure',
              label: 'Axure Components',
            },
            {
              value: 'sketch',
              label: 'Sketch Templates',
            },
            {
              value: 'docs',
              label: 'Design Documentation',
            },
          ],
        },
      ],
      props: "",
      viewer: null,
      cesiumLayerList: [],
    }
  },
  methods: {
    areaChange() {

    },
    imageryProvider(layers) {
      let url = "http://localhost:8080/geoserver/sicau/wms"

      let parameters = {
        service: 'WMS',
        format: 'image/png',
        transparent: true,
      }

      return new Cesium.WebMapServiceImageryProvider({url: url, layers: layers, parameters: parameters});
    },
    changeRiverLayer(checked, name) {
      console.log(name, checked)
      if (checked) {
        let yearList = ['2', '3', '5', '8']
        for (let year of yearList) {
          let layerName = name + year
          let imgLayer = this.viewer.imageryLayers.addImageryProvider(this.imageryProvider(layerName));
          this.cesiumLayerList.push({layerName, imgLayer})
        }
      }

      if (!checked) {
        for (let item of this.cesiumLayerList) {
          if (item.layerName.includes(name)) {
            this.viewer.imageryLayers.remove(item.imgLayer)
          }
        }
      }
    },

    changeOtherLayer(checked, layerName) {
      if (checked) {
        let imgLayer = this.viewer.imageryLayers.addImageryProvider(this.imageryProvider(layerName));
        this.cesiumLayerList.push({layerName, imgLayer})
      }
      if (!checked) {
        for (let item of this.cesiumLayerList) {
          if (item.layerName === layerName) {
            this.viewer.imageryLayers.remove(item.imgLayer)
          }
        }
      }
    },
  },

  mounted() {
    Cesium.Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI3YWEyMTRmZS0zNDI1LTQzY2ItODgyNy1jMjc4OGM2NDk2YWYiLCJpZCI6NzQ2ODcsImlhdCI6MTYzNzk3OTkxOH0.bcpqqEsuAJSOVVMs8y5FuaYl5GKUkdkN9-HPFWEo1J8';
    Cesium.Camera.DEFAULT_VIEW_RECTANGLE = Cesium.Rectangle.fromDegrees(80, 22, 130, 55)

    this.viewer = new Cesium.Viewer('cesiumContainer', {
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

    this.viewer.camera.flyTo({
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

.area-select-box {
  position: fixed;
  bottom: 0;
  right: 0;
  z-index: 999;
  font-size: 48px;
  color: white;
  text-align: center;
}

.layer-select-box {
  position: fixed;
  z-index: 999;
  display: flex;
  left: 10px;
  top: 10px;
  flex-direction: column;
  background-color: white;
  padding-left: 10px;
}
</style>
