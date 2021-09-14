<template>
  <div class="ui__wrapper">
    <v-app class="ui__element">
      <v-switch
        v-model="switch1"
        inset
        :color="ugcGreen"
        label="Energy Efficiency Measures"
        @click="toggleEfficiency"
      />
    </v-app>
    <v-app class="ui__element">
      <v-switch
        v-model="switch1"
        width:
        100%
        inset
        :color="ugcGreen"
        label="Flex Demand"
      />
    </v-app>
  </div>
</template>

<script>
export default {
  props: {
    map: {
      type: Object,
      required: true
    }
  },
  data: () => ({
    ugcGreen: '#C0D72D',
    layerIds: ['street-lights-height', 'street-lights-wattage'],
    switch1: true,
    switch2: true
  }),
  mounted () {
    this.map.on('load', () => { this.map.setLayoutProperty(this.layerIds[0], 'visibility', 'none') })
  },
  methods: {
    // toggleEfficiency () {
    //   const visibility = this.map.getLayoutProperty(
    //     this.layerIds[0],
    //     'visibility'
    //   )

    //   // Toggle layer visibility by changing the layout object's visibility property.
    //   if (visibility === 'visible') {
    //     this.map.setLayoutProperty(this.layerIds[0], 'visibility', 'none')
    //     this.className = ''
    //     this.switch1 = true
    //   } else {
    //     this.switch1 = false
    //     this.className = 'active'
    //     this.map.setLayoutProperty(
    //       this.layerIds[0],
    //       'visibility',
    //       'visible'
    //     )
    //   }
    // }
  }
}
</script>
<style scoped>
  .theme--dark{
    background:transparent !important;
  }
  /* .primary {
    background-color: red;
    border-color: red;
  } */
</style>
