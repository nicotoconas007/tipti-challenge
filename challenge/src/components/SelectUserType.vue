<template>
  <div class="container">
    <div>
      <select v-model="userType" @change="emitTypeUser">
        <option value="" v-if="userType == ''" selected disabled>
          Seleccione tipo de usuario
        </option>
        <option value="regular">Regular</option>
        <option value="reward">Reward</option>
      </select>
    </div>
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
