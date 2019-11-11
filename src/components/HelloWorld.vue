<template>
  <div class="hello">
    <div>{{msg}}</div>
    <div class="amap-wrapper" id="container"></div>
    <MyMap/>
  </div>
</template>

<script>
// import AMap from 'AMap'
import MyMap from './Map'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  methods: {
    // initMap () {
    //   let map = new AMap.Map('container', {
    //     zoom: 11, // 级别
    //     center: [116.397428, 39.90923], // 中心点坐标
    //     viewMode: '3D' // 使用3D视图
    //   })
    //   AMap.plugin(['AMap.ToolBar', 'AMap.Scale'], function () {
    //     map.addControl(new AMap.ToolBar())
    //     map.addControl(new AMap.Scale())
    //   })
    // }
  },
  mounted () {
    // this.initMap()
  },
  components: {
    MyMap
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.amap-wrapper {
  margin: auto;
  width: 500px;
  height: 500px;
}
</style>
