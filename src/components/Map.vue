<template>
  <div class="mapInit">
    <div id="container"></div>
  </div>
</template>

<script>
export default {
  name: 'mapInit',
  data () {
    return {
      Map: ''
    }
  },
  methods: {
    // 创建高德地图
    createdMap () {
      this.Map = new AMap.Map('container', {
        mapStyle: 'amap://styles/fresh',
        viewMode: '3D', // 使用3D视图
        pitch: 30 // 视野倾斜角度
      })
      // 设置地图缩放级别和中心点经纬度
      this.Map.setZoomAndCenter(18, [121.559868, 31.18244])
    },
    // 创建地图撒点,点击标注的点触发事件
    mapSprinkle () {
      let _this = this
      // 创建 AMap.Icon 实例：
      var icon = new AMap.Icon({
        size: new AMap.Size(50, 50), // 图标尺寸
        image: require('../assets/images/pic.png'), // Icon的图像
        imageOffset: new AMap.Pixel(10, 10), // 图像相对展示区域的偏移量，适于雪碧图等
        imageSize: new AMap.Size(30, 30), // 根据所设置的大小拉伸或压缩图片
        name: '上海'
      })
      let datad = [
        {
          address: [121.559868, 31.18244],
          style: '烟感',
          status: 1
        }, {
          address: [121.559811, 31.18224],
          style: '安防',
          status: 0
        }
      ]
      datad.map(function (item, index) {
        // 创建一个 Marker 实例：
        var marker = new AMap.Marker({
          position: item.address, // 经纬度对象，也可以是经纬度构成的一维数组[116.39, 39.9]
          icon: icon,
          // offset: new AMap.Pixel(-10, -10),
          anchor: 'center'
        })
        // 将创建的点标记添加到已有的地图实例:
        // 可以是一个对象，代表创建多个marker
        _this.Map.add(marker)
        // marker.setMap(_this.Map)
        // marker.setTitle("设置位置")
        marker.setLabel({
          // offset: new AMap.Pixel(15, 15),
          content: '定位名称'
        })
        // 点击标注的点触发事件
        // var clickHandler = function(e) { alert('您在[ '+e.lnglat.getLng()+','+e.lnglat.getLat()+' ]的位置点击了地图！') }
        // marker.on('click', clickHandler)
        AMap.event.addListener(marker, 'click', function (e) {
          let targetNode = e.target.He.icon.He
          console.log(targetNode.image, targetNode.name)
          // console.log(e.target.getPosition())   // 获取点击marker的经纬度
          _this.infor(e, item.style, item.status)
        })
      })
    },
    // 在点击marker的经纬度打开信息窗体
    infor (e, style, status) {
      if (status === 0) {
        style = '<p style="color:blue">' + style + '</p>'
      } else {
        style = '<p style="color:red">' + style + '</p>'
      }
      let infoWindow = new AMap.InfoWindow({
        offset: new AMap.Pixel(-15, -28),
        content: '<div style="width:210px height:60px line-height:20px overflow:auto">' + style + '</div>'
        // content: '这是信息窗体！这是信息窗体！'
      })
      infoWindow.open(this.Map, e.target.getPosition())
    }
  },
  created () {},
  mounted () {
    this.createdMap()
    this.mapSprinkle()
  }
}
</script>

<style lang="stylus" scoped>
.mapInit{
    width: 100%
    height: 100%
  #container {
    width: 100%
    height: 100%
  }
}
</style>
