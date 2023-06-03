<template>
  <div id="app">
    <SelectUserType @userType="receiveUser" />
    <InputDate @dates="receiveDates" />
    <CardHotel
      @hotels="receiveHotels"
      :userType="userType"
      :bestOption="bestOption"
      :error="error"
    />
    <button
      @click="calculateValue"
      v-show="bestOption == ''"
      :disabled="isInputDisabled"
    >
      Calcular
    </button>
    <button @click="viewAll" v-show="bestOption != ''">Ver todos</button>
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
      bestOption: "",
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
    viewAll() {
      this.bestOption = "";
    },
    calculateValue() {
      let minPrice = Number.MAX_VALUE;
      let totalStars = 0;
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
        hotel.stars > totalStars ? (totalStars = hotel.stars) : "";
        if (totalPrice < minPrice || (totalPrice === minPrice && hotel.stars === totalStars)) {
          minPrice = totalPrice;
          const hotelSelected = { ...hotel };
          hotelSelected.total = minPrice;
          hotelSelected.dates = this.dates;
          this.bestOption = hotelSelected;
        }
      });
    },
  },
  computed: {
    isInputDisabled() {
      return !this.userType || this.dates.length < 1 || this.error;
    },
  },
  watch: {
    dates: {
      handler() {
        this.bestOption ? this.calculateValue() : "";
      },
      deep: true,
    },
    userType: {
      handler() {
        this.bestOption ? this.calculateValue() : "";
      },
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
