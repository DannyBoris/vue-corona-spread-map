<template>
  <div class="slider">
    <VueSlideBar
      paddingless

      :range="range"
      @input="handleChange"
      :data="dates"
      :speed="0.1"
    />
    <h2 class="title">Presenting data for: {{ currDate }}</h2>
  </div>
</template>

<script>
import VueSlideBar from "vue-slide-bar";

export default {
  data() {
    return {

    };
  },
  computed: {
    range: function () {
      return this.dates.map((d) => {
        return { label: d };
      });
    },
  },
  methods: {
    handleChange: function (e) {
      this.dates.length && this.$emit("setDate", e || this.dates[0]);
    },
  },
  props: {
    dates: {
      type: Array,
    },
    currDate: {
      type: String,
    },
  },
  components: {
    VueSlideBar,
  },
};
</script>

<style>
.slider {
  width: 50%;
  margin: 0 auto;
}
.title {
  margin: 30px;
}
</style>