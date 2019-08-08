<template>
  <div class="v-input v-input--is-label-active v-input--is-dirty theme--light v-text-field v-text-field--is-booted">
    <div class="v-input__control">
      <div class="v-input__slot">
        <div class="v-text-field__slot"><label for="input-81" class="v-label v-label--active theme--light"
            style="left: 0px; right: auto; position: absolute;">*紧急程度</label>
          <span id="input-81" type="text">
            <v-radio-group v-model="row" row>
              <v-radio label="普通" value="1"></v-radio>
              <v-radio label="紧急" value="0"></v-radio>
            </v-radio-group>
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
    data: () => ({
      row: []
    }),
    methods: {}
  };
</script>
<style scoped>
  .v-text-field>.v-input__control>.v-input__slot:before {
    border-style: none;
  }
</style>