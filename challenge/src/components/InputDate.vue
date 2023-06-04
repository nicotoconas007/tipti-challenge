<template>
  <div class="container">
    <div class="mb-15">
      Seleccione fecha/s
    </div>
    <div class="container-input mb-15">
      <div v-for="(date, index) in dates" :key="index">
      <input class="border-general" type="date" v-model="date.date" />
      </div>
    </div>
    <div class="container-buttons">
      <button @click="addDate" :class="buttonClasses" :disabled="this.dates[0].date == '' || error">
        Agregar Fecha
      </button>
      <button @click="removeDate" class="org-color border-general" v-show="this.dates.length > 1">
        Eliminar fecha
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "InputDates",
  data() {
    return {
      dates: [{ date: "", isWeekend: false }],
      error: false,
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
    removeDate() {
      this.dates.pop();
    },
    isWeekend(dates) {
      dates.forEach((date) => {
        const day = new Date(date.date).toLocaleDateString("es-ES", {
          weekday: "long",
          timeZone: "UTC",
        });
        day === "sábado" || day === "domingo"
          ? (date.isWeekend = true)
          : (date.isWeekend = false);
      });
    },
    isEqualOrEmpty(dates) {
      const dateSet = new Set(dates.map(dateObj => dateObj.date));
      const emptyDate = dates.some(dateObj => dateObj.date === "");
      this.error = dates.length !== dateSet.size || emptyDate;
    }
  },
  computed: {
    buttonClasses() {
      return {
        'org-color': this.dates[0].date != "" && !this.error,
        'border-general': this.dates[0].date != "" && !this.error,
      };
    }
  },
  watch: {
    dates: {
      handler(newDates) {
        this.isWeekend(newDates);
        this.isEqualOrEmpty(newDates);
        this.$emit("dates", { selectedDates: newDates, error: this.error });
      },
      deep: true,
    },
  },
};
</script>

<style scoped>
  .container > div {
    color: #fff;
  }
  .container .container-input {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 15px;
  }
  .container .container-input input {
    width: 50vw;
    max-width: 200px;
    height: 30px;
    text-align: center;
  }
  .container .container-buttons {
    display: flex;
    justify-content: center;
    gap: 15px;
  }
  .container .container-buttons button {
    width: 40vw;
    max-width: 200px;
    height: 30px;
    transition: background-color 0.3s ease, color 0.3s ease;
  }
  .container .container-buttons button:hover:not(:disabled) {
    color: #fff !important;
    background-color: #af5700;
  }

</style>
