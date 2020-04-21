<template>
  <div class="home">
    <div id="map"></div>
  </div>
</template>

<script>
// @ is an alias to /src


export default {
  name: "Home",
  components: {},
  data() {
    return {
      map: null
    };
  },
  mounted() {
    this.initMap();
  },
  methods: {
    initMap() {
      let map = L.map("map", {
        minZoom: 3,
        maxZoom: 14,
        center: [39.550339, 116.114129],
        zoom: 12,
        zoomControl: false,
        attributionControl: false,
        crs: L.CRS.EPSG3857
      }).setView([39.9788, 116.30226], 14);
      this.map = map; //data上需要挂载
      window.map = map;
      // console.log(L.tileLayer)
      L.tileLayer.chinaProvider('TianDiTu.Normal.Map',{maxZoom:18,minZoom:5}).addTo(map);
    }
  }
};
</script>

<style lang="less" scoped>
#map {
  width: 100%;
  height: 100vh;
}
</style>
