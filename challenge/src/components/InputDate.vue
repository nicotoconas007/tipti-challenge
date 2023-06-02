<template>
  <div class="container">
    <div v-for="(date, index) in dates" :key="index">
      <input type="date" v-model="date.date" />
    </div>
  </div>
</template>

<script>
export default {
  name: "InputDates",
  data() {
    return {
      dates: [{ date: "", isWeekend: false }],
    };
  },
};
</script>
