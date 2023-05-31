<template>
  <div>
    <div id="map"></div>
  </div>
</template>
<script>
export default {
  name: "KakaoMap",
  data() {
    return {
      map: null,
    };
  },
  mounted() {
    if (window.kakao && window.kakao.maps) {
      this.loadMap();
    } else {
      this.loadScript();
    }
  },
  unmounted() {},
  methods: {
    loadScript() {
      const script = document.createElement("script");
      script.src =
        "//dapi.kakao.com/v2/maps/sdk.js?appkey=02645a7a8deefb78bea1a03e70b980f6&autoload=false";
      script.onload = () => window.kakao.maps.load(this.loadMap);
      document.head.appendChild(script);
    },
    loadMap() {
      const container = document.getElementById("map");
      const options = {
        center: new window.kakao.maps.LatLng(
          37.511124300023006,
          127.02175036116994
        ),

        level: 3,
      };
      this.map = new window.kakao.maps.Map(container, options);
      this.loadMaker();
    },
    loadMaker() {
      const marker = new window.kakao.maps.Marker({
        position: this.map.getCenter(),
      });
      marker.setMap(this.map);
    },
  },
};
</script>
<style scoped>
#map {
  min-width: 100vw;
  min-height: 100vh;
}
</style>
