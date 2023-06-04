<template>
  <div class="container">
    <div v-show="error" class="error mb-15">No se permiten fechas iguales o vacias.</div>
    <div class="container-cards">
      <div v-show="!bestOption" v-for="hotel in hotels" :key="hotel.name">
        <CardView :hotel="hotel" />
      </div>
    </div>
    <div v-show="bestOption && !error">
      <CardView :bestOption="bestOption" :userType="userType" />
    </div>
  </div>
</template>

<script>
import CardView from './CardView.vue';
export default {
  name: "HotelOption",
  props: ["bestOption", "userType", "error"],
  components: {
    CardView
  },  
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

<style scoped>
  .container .error {
    font-size: 16px;
    background-color: #ffcccc;
    padding: 11px;
    border-radius: 5px;
  }
  .container .container-cards {
    display: flex;
    justify-content: center;
    gap: 50px;
    max-width: 1500px;
    flex-wrap: wrap;
    margin-top: 15px;
  }
</style>
