<template>
  <div class="container">
    <div v-for="(date, index) in dates" :key="index">
      <input type="date" v-model="date.date" />
    </div>
    <button @click="addDate" :disabled="this.dates[0].date == ''">
      Agregar Fecha
    </button>
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
  methods: {
    addDate() {
      const lastDate = this.dates[this.dates.length - 1];
      const nextDate = new Date(lastDate.date);
      nextDate.setDate(nextDate.getDate() + 1);
      this.dates.push({
        date: nextDate.toISOString().substring(0, 10),
        isWeekend: false,
      });
    },
  },
};
</script>
