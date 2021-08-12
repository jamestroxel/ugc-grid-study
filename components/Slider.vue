<template>
  <div class="ui__wrapper">
    <div class="slider__wrapper">
      <v-app>
        <v-slider
          v-model="fruits"
          :color="white"
          :tick-labels="ticksLabels"
          :max="4"
          step="1"
          ticks="always"
          @change="emitToParent"
        />
      </v-app>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    white: '#4af2a1',
    value: 0,
    fruits: 0,
    ticksLabels: [
      '0%',
      '25%',
      '50%',
      '75%',
      '100%'
    ]
  }),

  methods: {
    emitToParent (event) {
      this.$emit('childToParent', this.ticksLabels[event])
    }
  }
}
</script>
<style scoped>
  .v-application{
    background:transparent !important;
  }
  /* .primary {
    background-color: red;
    border-color: red;
  } */
</style>
