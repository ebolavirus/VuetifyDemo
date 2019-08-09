<template>
  <div class="v-input v-input--is-label-active v-input--is-dirty v-text-field v-text-field--is-booted">
    <div class="v-input__control">
      <div class="v-input__slot">
        <div class="v-text-field__slot"><label for="input-81" class="v-label v-label--active"
            style="left: 0px; right: auto; position: absolute;">{{titleValue}}</label>
          <span id="input-81" type="text">
            {{realValue}}
          </span>
        </div>
      </div>
      <!-- <div class="v-text-field__details">
        <div class="v-messages">
          <div class="v-messages__wrapper"></div>
        </div>
      </div> -->
    </div>
  </div>
</template>

<script>
  export default {
    components: {},
    props: {
      titleValue: {
        type: String,
        default: ''
      },
      realValue: {
        type: String,
        default: ''
      }
    },
    data: () => ({}),
    methods: {}
  };
</script>
<style scoped>
  .v-text-field>.v-input__control>.v-input__slot:before {
    border-style: none;
  }
</style>