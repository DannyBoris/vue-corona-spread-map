
<template>
  <div class="map-container">
    <MglMap
      :zoom="zoom"
      :center="center"
      :accessToken="accessToken"
      :mapStyle="mapStyle"
    >
      <Markers :currDate="currDate" :places="places" />
    </MglMap>
  </div>
</template>

<script>
import Mapbox from "mapbox-gl";
import Markers from "./Markers";
import { MglMap } from "vue-mapbox";

export default {
  components: {
    MglMap,
    Markers,
  },
  props: {
    places: {
      type: Array,
    },
    currDate: {
      type: String,
    },
  },
  data() {
    return {
      center: [this.places[0].X, this.places[0].Y],
      zoom: 6,
      accessToken:
        "pk.eyJ1IjoiZGFubnlib3JpcyIsImEiOiJja2dpZHlhcTIwa2lpMnJxbjZlY3MzcXVwIn0.clZ-JQvOxBUevYDZpgHtYw", // your access token. Needed if you using Mapbox maps
      mapStyle: "mapbox://styles/mapbox/streets-v11", // your map style
    };
  },

  created() {
    // We need to set mapbox-gl library here in order to use it in template
    this.mapbox = Mapbox;
  },
};
</script>

<style scoped>
.map-container {
  height: 70vh;
  margin: 0 auto;
  width: 50%;
}

</style>