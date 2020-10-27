<template>
  <div class="date-control">
    <DateSlider :dates="dates" />
    <div class="date-container">
      <div :ref="date" class="control" v-for="date in dates" :key="date">
        <label :for="date">{{ date }}</label>
        <input
          hidden
          @change="setCurrDate"
          name="date"
          :id="date"
          type="radio"
        />
      </div>
    </div>
    <h2>
      Presenting Data from <span class="current-date">{{ dateToDisplay }}</span>
    </h2>
  </div>
</template>

<script>
import DateSlider from "./DateSlider";
export default {
  components: {
    DateSlider,
  },
  props: {
    dates: {
      type: Array,
    },
    currDate: {
      type: String,
    },
  },
  computed: {
    dateToDisplay: function () {
      return this.currDate;
    },
  },
  methods: {
    setCurrDate: function (e) {
      this.$emit("setDate", e.target.id);
    },
  },
};
</script>

<style scoped>
.date-container {
  display: flex;
}
.date-control {
  display: flex;
  flex-direction: column;
  margin: 0.5rem 0;
  justify-content: center;
  align-items: center;
}
.control {
  height: 30px;
  display: flex;
  align-items: center;
  font-size: 0.65rem;
  font-weight: 700;
  border: 1px solid;
  border-radius: 6px;
  margin: 0 0.5rem;
}
.control > label {
  padding: 0.6rem;
}
.current-date {
  color: orange;
}
</style>