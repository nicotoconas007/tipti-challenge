<template>
  <div class="container">
    <div v-show="!bestOption" v-for="hotel in hotels" :key="hotel.name">
      {{ hotel.name }}
    </div>
    <div v-show="bestOption">
      <div>{{ bestOption.name }} - {{ bestOption.total }} - {{ userType }}</div>
      <span v-for="(date, index) in bestOption.dates" :key="index">
        {{ date.date }}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardHotel",
  props: ["bestOption", "userType"],
  data() {
    return {
      hotels: [
        {
          name: "Lakewood",
          stars: 3,
          regularPrice: 110,
          rewardPrice: 80,
          weekendRgPrice: 90,
          weekendRwPrice: 80,
        },
        {
          name: "Bridgewood",
          stars: 4,
          regularPrice: 160,
          rewardPrice: 110,
          weekendRgPrice: 60,
          weekendRwPrice: 50,
        },
        {
          name: "Ridgewood",
          stars: 5,
          regularPrice: 220,
          rewardPrice: 100,
          weekendRgPrice: 150,
          weekendRwPrice: 40,
        },
      ],
    };
  },
  mounted() {
    this.emitHotels();
  },

  methods: {
    emitHotels() {
      this.$emit("hotels", this.hotels);
    },
  },
};
</script>
