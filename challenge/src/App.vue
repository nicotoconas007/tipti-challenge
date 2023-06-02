<template>
  <div id="app">
    <SelectUserType @userType="receiveUser" />
    <CardHotel @hotels="receiveHotels"/>
    <InputDate />
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
      hotels: []
    };
  },

  methods: {
    receiveUser(userType) {
      this.userType = userType
    },
    receiveHotels(hotels) {
      this.hotels = hotels
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
