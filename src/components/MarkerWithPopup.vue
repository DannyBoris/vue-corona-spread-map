<template>
  <div>
    <MglMarker
      @mouseenter="open"
      @mouseleave="close"
      :coordinates="[place.X, place.Y]"
      color="red"
    >
      <div
        :style="{
          background: getColor(this.confirmedCases),
          width: Math.sqrt(confirmedCases) / 4 + 'px',
          height: Math.sqrt(confirmedCases) / 4 + 'px',
        }"
        class="marker-circle"
        slot="marker"
      ></div>
      <MglPopup
        :showed="isPopupOpen"
        anchor="left"
        :coordinates="[place.X, place.Y]"
      >
        <div class="tooltip-container">
          <h2 class="city-name">{{ place.DisplayName }}</h2>
          <span>{{ `${place[currDate + "_Rate"]}` }} Rate</span>
          <span> Confirmed Cases - {{ confirmedCases }} </span>
        </div>
      </MglPopup>
    </MglMarker>
  </div>
</template>

<script>
import { MglMarker, MglPopup } from "vue-mapbox";

export default {
  data() {
    return {
      isPopupOpen: false,
      confirmedCases: this.place[this.currDate + "_Confirmed_Cases"],
    };
  },

  components: {
    MglMarker,
    MglPopup,
  },
  props: {
    place: {
      type: Object,
    },
    currDate: {
      type: String,
    },
  },
  methods: {
    getColor: function (cases) {
      switch (true) {
        case cases < 4000:
          return "rgba(0, 230, 64, .7)";
        case cases < 10000:
          return "rgba(238, 238, 0, .7)";
        case cases < 20000:
          return "rgba(249, 105, 14,.7)";
        case cases > 20000:
          return "rgba(207, 0, 15,.7)";
        default:
          return "gray";
      }
    },
    open: function () {
      this.isPopupOpen = true;
    },
    close: function () {
      this.isPopupOpen = false;
    },
  },
};
</script>

<style scoped>
.tooltip-container {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
.city-name {
  text-align: center;
  width: 100%;
  margin: 0;
  padding: 10px 0;
}
.marker-circle {
  border-radius: 100px;
}
</style>