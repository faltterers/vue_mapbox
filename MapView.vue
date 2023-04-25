<template>
    <div class="box">
        <div id="mapbox"></div>
    </div>
</template>
<script >
import mapboxgl from 'mapbox-gl';
import 'mapbox-gl/dist/mapbox-gl.css';
import MapboxLanguage  from '@mapbox/mapbox-gl-language'

export default {
    name:"MapBox",
    data: () => ({
        map: null
    }),
    methods: {
        initMap(){
            mapboxgl.accessToken ='pk.eyJ1IjoiemgwMSIsImEiOiJjbGd2b3NnZzIwNDB2M2xvOTZ5czVjeXp4In0.NVLrwmiFkkeS1y2JIRvI7Q'; 
            var map = new mapboxgl.Map({
                container: 'mapbox', // container id 绑定的组件的id
                style: 'mapbox://styles/mapbox/dark-v11', //地图样式，可以使用官网预定义的样式,也可以自定义
                center: [120.2,30.1666], // 初始地图中心点位置
                zoom: 3,     // starting zoom 地图初始的层级
                // pitch: 60,  //地图的角度，不写默认是0，取值是0-60度，一般在3D中使用
                bearing: 0, //地图的初始方向，值是北的逆时针度数，默认是0，即是正北
                // antialias: true, //抗锯齿，通过false关闭提升性能 
                zoomControl: true,
            }); 
            // 设置语言
            mapboxgl.setRTLTextPlugin('https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-rtl-text/v0.2.3/mapbox-gl-rtl-text.js');
            map.addControl(new MapboxLanguage({
                defaultLanguage: 'zh-Hans'
            }));


            // 导航控制条
            var nav = new mapboxgl.NavigationControl();
            map.addControl(nav, 'top-right'); 

            //去除mapbox的logo
            map._logoControl && map.removeControl(map._logoControl);

        }
    },
    mounted(){
        this.initMap();
    }
}
</script>
<style>

*{  
    margin: 0;
    height: 100%;
}

#mapbox{
    height: 100%;
    top: 0;
    bottom: 0;
    position:absolute;
    width: 100vw;
}

.mapboxgl-ctrl-top-right{
    height: 9.5%;
}
.mapboxgl-ctrl-bottom-right{
    display: none;
}
</style>