<template>
  <div class="v-input v-input--is-label-active v-input--is-dirty theme--light v-text-field v-text-field--is-booted">
    <div class="v-input__control">
      <div class="v-input__slot">
        <div class="v-text-field__slot"><label for="input-81" class="v-label v-label--active theme--light"
            style="left: 0px; right: auto; position: absolute;">*办公室位置(只读)</label>
          <span id="input-81" type="text">
            信息中心十五六
          </span>
        </div>
      </div>
      <div class="v-text-field__details">
        <div class="v-messages theme--light">
          <div class="v-messages__wrapper"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    components: {},
    data: () => ({}),
    methods: {}
  };
</script>
<style scoped>
  .v-text-field>.v-input__control>.v-input__slot:before {
    border-style: none;
  }
</style>