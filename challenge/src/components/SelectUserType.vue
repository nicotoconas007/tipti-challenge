<template>
  <div class="container mb-15">
      <div class="mb-15">Seleccione el tipo de usuario</div>
      <select v-model="userType" @change="emitTypeUser" class="border-general">
        <option value="" v-if="userType == ''" selected disabled>
          Seleccione
        </option>
        <option value="regular">Regular</option>
        <option value="reward">Reward</option>
      </select>
  </div>
</template>

<script>
export default {
  name: "SelectUserType",
  data() {
    return {
      userType: "",
    };
  },
  methods: {
    emitTypeUser() {
        this.$emit('userType', this.userType);
    }
  },
};
</script>

<style scoped>
  .container > div {
    color: #fff;
  }
  .container select {
    max-width: 300px;
    width: 50vw;
    height: 30px;
    border-radius: 4px;
    background-color: #fff;
    color: #000;
    text-align: center;
  }
  .container select option {
    color: #000;
    background-color: #fff;
    font-size: 14px;
  }
</style>
