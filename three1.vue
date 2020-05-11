<template>
<div>
    <div id='viewer'>
        <div id="lorem-content"></div>
    </div>
   
    </div>
</template>
<script>
import PhotoSphereViewer from 'photo-sphere-viewer'
    import 'uevent/uevent.js'
    import 'photo-sphere-viewer/dist/photo-sphere-viewer.css'


export default {
    name: "PSViewer",

    data() {
        return {
            width:798,
            height:498,
            img:require('../assets/1.jpg'),
            marker:require('../assets/logo.png'),
            // PSV:PhotoSphereViewer
        };
    },
    methods: {
    add(e){
    
     this.PSV.addMarker({
    id: '#' + Math.random(),
    longitude: e.longitude,
    latitude: e.latitude,
    image: this.marker,
    width: 32,
    height: 32,
    anchor: 'bottom center',
    tooltip: 'Generated pin',
    data: {
      generated: true
    }
  });

    },
    remove(marker){
       
  if (marker.data && marker.data.generated) {
    this.PSV.removeMarker(marker);
  
}
    },
        // photo-sphere-viewer
        init:function(){
    
　　　　this.PSV = PhotoSphereViewer({
　　　　　　container: document.getElementById('viewer'),
　　　　　　panorama: this.img,
　　　　　　size: {
　　　　　　　　width: '100%',
　　　　　　　　height: screen.availHeight
　　　　　　},
　　　　　　// caption: '厂区鸟瞰图',
　　　　　　caption: ' ',
　　　　　　time_anim: false,
　　　　　　default_long: 1.4441088145446443,
　　　　　　default_lat: 0.0800613513013615,
　　　　　　sphere_correction: {pan: 30.01, tilt: 0, roll: 0},
　　　　　　// max_fov: 100, // 最大缩放值
　　　　　　// min_fov: 99, // 最小缩放值
　　　　　　default_fov: 100, // 默认缩放值，在1-179之间
　　　　　　// latitude_range: [0,0],//禁止上下滑动
　　　　　　// mousewheel: false, // 禁止鼠标滚轮缩放
　　　　　　// navbar: false,
　　　　　　navbar: [
　　　　　　　　'autorotate',
　　　　　　　　'zoom',
　　　　　　　　'markers',
　　　　　　　　'caption',
　　　　　　　　'fullscreen'
　　　　　　],
　　　　　　theta_offset: 1000, // 旋转速度
　　　　　　// markers: this.markersData
markers: [
    {
      // image marker that opens the panel when clicked
      id: 'dsf',
      longitude: 0.2,
      latitude: -0.13770,
      image: this.marker,
      width: 32,
      height: 32,
      anchor: 'bottom center',
      tooltip: 'A image marker. <b>Click me!</b>',
     content: document.getElementById('lorem-content').innerHTML
    },
  ]
  })
   
　 this.PSV.on('click',this.add );

/**
 * Delete a generated marker when the user clicks on it
 */
this.PSV.on('select-marker', this.remove);

        },

   all(){
       this.init();
    //    var can=document.getElementById('viewer');
    //    can.addEventListener('click',this.add,false)
   }
    },
mounted(){
        this.all();
    },
beforeDestory(){}
};
</script>
<style lang='scss'  scoped>

</style>