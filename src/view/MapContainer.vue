<template>
  <div class="home_div">
    <div class="map_title">
      <h3>设备维护展示</h3>
    </div>
    <div id="container">

    </div>
  </div>
</template>
<script>
import AMapLoader from '@amap/amap-jsapi-loader';
// import logo from '@/assets/logo.png';
import wrench from '@/assets/wrench.png';
import bj from '@/assets/bj.png';
import wrenchMan from '@/assets/wrenchMan.png';

export default {
  name: "Mapview",
  data() {
    return {
      //map:null,
    }
  },
  created() {

  },
  mounted() {
    this.initAMap();
  },
  methods: {
    addicon1() {


      var icon = new AMap.Icon({
        // 图标尺寸
        size: new AMap.Size(35, 35),
        // 图标的原点
        anchor: 'bottom-center',
        // 图标的取图地址
        image: wrench,
        // 图标所用的图片大小
        imageSize: new AMap.Size(35, 35)
      });
      // 创建一个Marker实例：
      var marker = new AMap.Marker({
        position: new AMap.LngLat(120.70648, 28.00109), // 标记位置
        icon: icon,  // 使用自定义图标
        title: '维护位置',
        clickable: true,
        offset: new AMap.Pixel(17,-35), // 设置点标记偏移量
        anchor:'top-center', // 设置锚点方位
      });
      marker.setLabel({
        offset: new AMap.Pixel(-35, 30),  //设置文本标注偏移量
        content: "<div class='info'>正在维修</div>", //设置文本标注内容
        direction: 'right' //设置文本标注方位
      });
      this.map.add(marker);
    },
    addicon2() {


      var icon = new AMap.Icon({
        // 图标尺寸
        size: new AMap.Size(35, 35),
        // 图标的原点
        anchor: 'bottom-center',
        // 图标的取图地址
        image: bj,
        // 图标所用的图片大小
        imageSize: new AMap.Size(35, 35)
      });
      // 创建一个Marker实例：
      var marker = new AMap.Marker({
        position: new AMap.LngLat(86.87219 , 40.44667), // 标记位置
        icon: icon,  // 使用自定义图标
        clickable: true,
        offset: new AMap.Pixel(17,-35), // 设置点标记偏移量
        anchor:'top-center', // 设置锚点方位
      });
      marker.setLabel({
        offset: new AMap.Pixel(-35, 30),  //设置文本标注偏移量
        content: "<div class='info'>异常</div>", //设置文本标注内容
        direction: 'right' //设置文本标注方位
      });
      this.map.add(marker);
    },  addicon3() {


      var icon = new AMap.Icon({
        // 图标尺寸
        size: new AMap.Size(35, 35),
        // 图标的原点
        anchor: 'bottom-center',
        // 图标的取图地址
        image: wrenchMan,
        // 图标所用的图片大小
        imageSize: new AMap.Size(35, 35)
      });
      // 创建一个Marker实例：
      var marker = new AMap.Marker({
        position: new AMap.LngLat(103.73159 , 33.03584), // 标记位置
        icon: icon,  // 使用自定义图标
        clickable: true,
        offset: new AMap.Pixel(17,-35), // 设置点标记偏移量
        anchor:'top-center', // 设置锚点方位
      });
      marker.setLabel({
        offset: new AMap.Pixel(-35, 30),  //设置文本标注偏移量
        content: "<div class='info'>调度中</div>", //设置文本标注内容
        direction: 'right' //设置文本标注方位
      });
      this.map.add(marker);
    },
    addpolyline() {
      var path = [
        new AMap.LngLat(116.368904, 39.913423),
        new AMap.LngLat(120.70648, 28.00109),

      ];

// 创建折线实例
      var polyline = new AMap.Polyline({
        path: path,
        showDir: true,
        strokeStyle: "dashed",
        borderWeight: 2, // 线条宽度，默认为 1
        strokeColor: 'blue', // 线条颜色
        lineJoin: 'round' // 折线拐点连接处样式
      });
      this.map.add(polyline);

    },
    addpolyline2() {
      var path = [
        new AMap.LngLat(116.45504, 26.97543),
        new AMap.LngLat(86.87219 , 40.44667),

      ];

// 创建折线实例
      var polyline = new AMap.Polyline({
        path: path,
        showDir: true,
        strokeStyle: "dashed",
        borderWeight: 2, // 线条宽度，默认为 1
        strokeColor: 'blue', // 线条颜色
        lineJoin: 'round' // 折线拐点连接处样式
      });
      this.map.add(polyline);

    },
    initAMap() {
      AMapLoader.load({
        key: '3774a3f0cdaeede4cb761c2ae15c0e29',  //设置您的key
        version: "2.0",
        plugins: ['AMap.ToolBar', 'AMap.Driving'],
        AMapUI: {
          version: "1.1",
          plugins: [],

        },
        Loca: {
          version: "2.0"
        },
      }).then((AMap) => {
        this.map = new AMap.Map("container", {
          viewMode: "3D",
          zoom: 5,
          zooms: [2, 22],
          center: [105.602725, 37.076636],
        });
        this.addicon1()
        this.addicon2()
        this.addicon3()
        this.addpolyline()
        this.addpolyline2()

      }).catch(e => {
        console.log(e);
      })
    },
  }


}
</script>
<style scoped>
.home_div {
  padding: 0px;
  margin: 0px;
  width: 100%;
  height: 100%;
  position: relative;
}

#container {
  padding: 0px;
  margin: 0px;
  width: 100%;
  height: 100%;
  position: absolute;
}

.map_title {
  position: absolute;
  z-index: 1;
  width: 100%;
  height: 50px;
  background-color: rgba(27, 25, 27, 0.884);

}

h3 {
  position: absolute;
  left: 10px;
  z-index: 2;
  color: white;
}
</style>