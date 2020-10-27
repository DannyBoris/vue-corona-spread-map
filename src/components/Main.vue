<template>
  <div class="main">
    <DateSlider v-if="currDate" :currDate="currDate" @setDate="onSetDate" :dates="dates" />
    <Map :currDate="currDate" v-if="places.length" :places="places" />
  </div>
</template>

<script>
import Map from "./Map";
import DateSlider from "./DateSlider";
export default {
  components: {
    Map,
    DateSlider,
  },
  data() {
    return {
      places: [],
      dates: [],
      currDate: "2020/10/14", // try to use computed and take first value from dates
    };
  },

  // computed: {
  //   // set initial date
  //   currDate: {
  //     get: function () {
  //       return this.dates[0];
  //     },
  //     set: function (newDate) {
  //       return newDate;
  //     },
  //   },
  // },

  methods: {
    //Get data from the json file and set it to local state as places.
    getData: async function () {
      let res = await fetch("../data.json");
      let data = await res.json();
      this.places = data;
      this.setDates(); // set dates after getting the places array.
    },
    setDates: function () {
      this.dates = Object.keys(this.places[0])
        .filter((k) => k.includes("2020" && "Rate")) // just to filter out the dates.
        .map((d) => d.split("_")[0]);
    },
    //From date conrol component, get an event and sets date to filter by.
    onSetDate: function (newDate) {
      this.currDate = newDate;
    },
  },
  created() {
    //Get data when component created
    this.getData();
  },
};
</script>

<style>
</style>