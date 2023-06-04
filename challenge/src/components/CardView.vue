<template>
  <div>
    <div class="card-container">
      <div class="card-name mb-15">Hotel {{ hotel ? hotel.name : bestOption.name }}</div>
      <div v-if="hotel" class="card-stars mb-15">
        <hr>
        <svg v-for="stars in hotel.stars" :key="stars" xmlns="http://www.w3.org/2000/svg" height="1em" viewBox="0 0 576 512" fill="yellow">
          <path d="M316.9 18C311.6 7 300.4 0 288.1 0s-23.4 7-28.8 18L195 150.3 51.4 171.5c-12 1.8-22 10.2-25.7 21.7s-.7 24.2 7.9 32.7L137.8 329 113.2 474.7c-2 12 3 24.2 12.9 31.3s23 8 33.8 2.3l128.3-68.5 128.3 68.5c10.8 5.7 23.9 4.9 33.8-2.3s14.9-19.3 12.9-31.3L438.5 329 542.7 225.9c8.6-8.5 11.7-21.2 7.9-32.7s-13.7-19.9-25.7-21.7L381.2 150.3 316.9 18z"/>
        </svg>
      </div>
      <div v-if="bestOption">
        <div class="title-prices">Precio: ${{ bestOption.total }}</div>
        <hr>
        <div class="selected-dates">
          <span v-if="bestOption.dates.length > 1">Fechas seleccionadas: </span>
          <span v-else>Fecha seleccionada: </span>
        </div>
        <span class="dates" v-for="(date, index) in bestOption.dates" :key="index">
          {{ date.date }}
        </span>
      </div>
      <div v-if="hotel" class="card-prices">
        <div class="title-prices">Precios:</div>
        <div class="card-user">Usuario regular:</div>
        <span>Dia de semana regular: ${{ hotel.regularPrice }}</span>
        <span>Fin de semana regular: ${{ hotel.weekendRgPrice}}</span>
        <hr>
        <div class="card-user">Usuario reward:</div>
        <span>Dia de semana reward: ${{ hotel.rewardPrice }}</span>
        <span>Fin de semana reward: ${{ hotel.weekendRwPrice }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardView",
  props: ["hotel", "bestOption"],
};
</script>

<style scoped>
.card-container {
  padding: 50px;
  background-color: #af5700;
  border-radius: 5px;
  cursor: pointer;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  max-width: 350px;
  color: #fff;
}

.card-container:hover {
  transform: scale(1.05);
}

.card-container .card-name {
  font-size: 24px;
  font-weight: bold;
}
.card-container .selected-dates {
  font-weight: bold;
  margin-bottom: 5px;
}
.card-container .dates {
  display: block;
  margin-top: 2px;
}
.card-container .title-prices{
  font-weight: bold;
  font-size: 18px;
  margin-bottom: 8px;
  align-self: center;
}
.card-container .card-prices {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.card-container .card-prices .card-user {
  align-self: center;
  font-size: 18px;
  margin-bottom: 5px;
  font-weight: bold;
}
.card-container .card-prices span {
  font-size: 16px;
  margin-bottom: 5px;
}

</style>
