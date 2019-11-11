# 引入高德地图 API

```HTML
<!-- 根目录 index.html -->
<script type="text/javascript" src="https://webapi.amap.com/maps?v=1.4.15&key=youkey"></script>
```

```JavaScript
// webpack.base.conf
module.exports = {
  externals: {
    'AMap': 'AMap'
  }
}
```

```JavaScript
// 组件内使用
import AMap from 'AMap'

initMap () {
  let map = new AMap.Map('container', {
    zoom: 11, // 级别
    center: [116.397428, 39.90923], // 中心点坐标
    viewMode: '3D' // 使用3D视图
  })
  AMap.plugin(['AMap.ToolBar', 'AMap.Scale'], function () {
    map.addControl(new AMap.ToolBar())
    map.addControl(new AMap.Scale())
  })
}
```
