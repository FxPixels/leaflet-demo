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

      // 地图类型
      L.tileLayer
        .chinaProvider("GaoDe.Normal.Map", {
          maxZoom: 18,
          minZoom: 5,
          attribution: "fxpixels"
        })
        .addTo(map);

      L.tileLayer
        .chinaProvider("GaoDe.Satellite.Annotion", {
          maxZoom: 18,
          minZoom: 5
        })
      .addTo(map);

      // 标签
      var myIcon = L.icon({
        iconUrl:
          "https://unpkg.com/leaflet@1.6.0/dist/images/marker-icon-2x.png",
        iconSize: [28, 42],
        iconAnchor: [16, 42],
        popupAnchor: [-3, -46],
        // shadowUrl:
        //   "https://unpkg.com/leaflet@1.6.0/dist/images/marker-icon-2x.png",
        shadowSize: [68, 95],
        shadowAnchor: [22, 94]
      });

      // popup
      L.marker([39.959205, 116.342361], { icon: myIcon })
        .addTo(map)
        .bindPopup("<b>Hello world!</b><br />I am a popup.")
        .openPopup();

      // tooltip
      L.marker([39.95737, 116.353482], {
        icon: myIcon,
        direction: "center"
      })
        .addTo(map)
        .bindTooltip("my tooltip text", { direction: "bottom" })
        .openTooltip();
      L.tooltip();

      // 圆环
      L.circle([39.971439, 116.318224], 500, {
        color: "red",
        fillColor: "#f03",
        fillOpacity: 0.5
      })
        .addTo(map)
        .bindPopup("I am a circle.");

      // 自定多边形
      L.polygon([
        [39.974868, 116.354617],
        [39.975132, 116.369202],
        [39.968286, 116.369631],
        [39.968155, 116.356933],
        [39.968945, 116.355132]
      ])
        .addTo(map)
        .bindPopup("I am a polygon.");

      // 点击气泡
      let popup = L.popup();
      function onMapClick(e) {
        popup
          .setLatLng(e.latlng)
          .setContent("You clicked the map at " + e.latlng.toString())
          .openOn(map);
      }
      map.on("click", onMapClick);
    }
  }
};
</script>

<style lang="less" scoped>
#map {
  width: 100%;
  height: 100vh;
  box-sizing: border-box;
}
</style>
