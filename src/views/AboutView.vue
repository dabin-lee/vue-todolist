<template>
  <div class="about">
    <h1>{{ getDateAndTime(createAt) }}</h1>
  </div>
</template>

<script>
import { dataFormat } from "../mixins/dateFormat";
export default {
  data() {
    return {
      createAt: {},
    };
  },
  // method: {
  //   getDateAndTime(date) {
  //     let hour = date.getHours();
  //     let minutes = date.getMinutes();
  //     let fullDate = `${date.getFullYear()} / ${
  //       date.getMonth() + 1
  //     } / ${date.getDate()}`;
  //     return `${fullDate} ${hour}: ${minutes}`;
  //   },
  // },
  created() {
    this.createAt = new Date();
  },
  mixins: [dataFormat],
};
</script>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
