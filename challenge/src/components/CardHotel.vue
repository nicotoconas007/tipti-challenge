<template>
  <div class="container">
    <div v-for="hotel in hotels" :key="hotel.name">
      {{ hotel.name }}
    </div>
  </div>
</template>

<script>
export default {
  name: "CardHotel",
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
