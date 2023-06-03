<template>
  <div id="app">
    <SelectUserType @userType="receiveUser" />
    <InputDate @dates="receiveDates" />
    <CardHotel @hotels="receiveHotels" :userType="userType" :bestOption="bestOption" />
    <button @click="calculateValue">Calcular</button>
  </div>
</template>

<script>
import CardHotel from "./components/CardHotel.vue";
import InputDate from "./components/InputDate.vue";
import SelectUserType from "./components/SelectUserType.vue";
export default {
  name: "App",
  components: {
    CardHotel,
    InputDate,
    SelectUserType,
  },
  data() {
    return {
      userType: "",
      hotels: [],
      dates: [],
      error: false,
      bestOption: ''
    };
  },

  methods: {
    receiveUser(userType) {
      this.userType = userType;
    },
    receiveHotels(hotels) {
      this.hotels = hotels;
    },
    receiveDates(dates) {
      this.dates = dates.selectedDates;
      this.error = dates.error;
    },
    calculateValue() {
      let minPrice = Number.MAX_VALUE;
      this.hotels.forEach((hotel) => {
        let totalPrice = 0;
        this.dates.forEach((date) => {
          if (this.userType === "regular") {
            totalPrice += date.isWeekend
              ? hotel.weekendRgPrice
              : hotel.regularPrice;
          } else {
            totalPrice += date.isWeekend
              ? hotel.weekendRwPrice
              : hotel.rewardPrice;
          }
        });
        if (totalPrice < minPrice) {
          minPrice = totalPrice;
          const hotelSelected = { ...hotel };
          hotelSelected.total = minPrice;
          hotelSelected.dates = this.dates;
          this.bestOption = hotelSelected;
        }
      });
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
