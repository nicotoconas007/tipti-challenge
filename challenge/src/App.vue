<template>
  <div id="app">
    <SelectUserType @userType="receiveUser" />
    <InputDate @dates="receiveDates" />
    <button
      @click="calculateValue"
      v-show="bestOption == ''"
      :disabled="isInputDisabled"
      :class="{'primary-button' : !isInputDisabled}"
    >
      Ver mejor opcion
    </button>
    <button @click="viewAll" v-show="bestOption != ''" class="primary-button">
      Ver todos
    </button>
    <HotelOption
      @hotels="receiveHotels"
      :userType="userType"
      :bestOption="bestOption"
      :error="error"
    />
  </div>
</template>

<script>
import HotelOption from "./components/HotelOption.vue";
import InputDate from "./components/InputDate.vue";
import SelectUserType from "./components/SelectUserType.vue";
export default {
  name: "App",
  components: {
    HotelOption,
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
html {
  background: url("./assets/img/background.png");
  background-size: cover;
  background-color: #000;
  background-repeat: no-repeat;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}
#app button:nth-child(3), #app button:nth-child(4) {
  max-width: 500px;
  width: 50vw;
  height: 40px;
  margin-top: 15px;
  border-radius: 20px;
  border: 0;
  background-color: #e3e3e3;
}
#app .primary-button {
  background-color: #141435 !important;
  cursor: pointer;
  transition: background-color 0.3s ease, color 0.3s ease;
  color: #fff;
}
#app .primary-button:hover:not(:disabled) { 
  background-color: #af5700 !important;
}
.org-color {
  color: #af5700 !important;
}
.mb-15 {
  margin-bottom: 15px !important;
}
.border-general {
  border-radius: 5px !important;
  border: 1px solid #af5700 !important;
  cursor: pointer !important;
}

@media screen and (max-width: 768px) {
  html {
    background: #FF914D;
  }
}

</style>
