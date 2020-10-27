<template>
  <div class="markers">
    <div class="marker" v-for="place in places" :key="place.id">
      <MarkerWithPopup :place="place" :currDate="currDate" />
    </div>
  </div>
</template>

<script>
import MarkerWithPopup from "./MarkerWithPopup";
export default {
  components: {
    MarkerWithPopup,
  },
  name: "Markers",
  props: {
    places: {
      type: Array,
    },
    currDate: {
      type: String,
    },
  },
};
</script>

<style scoped>

</style>