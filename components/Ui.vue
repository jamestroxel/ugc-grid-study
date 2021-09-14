<template>
  <div class="ui__wrapper">
    <div class="ui__element">
      <v-app>
        <v-card-text>
          <p class="ui__title">
            Adoption
          </p>
          <v-slider
            v-model="electrification"
            :color="ugcGreen"
            :tick-labels="ticksLabels"
            :max="4"
            step="1"
            ticks="always"
            @change="onChildClick"
          />
        </v-card-text>
        <v-card-text>
          <p class="ui__title">
            Scenarios
          </p>
          <v-switch
            v-model="switch1"
            inset
            :color="ugcGreen"
            label="Energy Efficiency Measures"
            @click="toggleEfficiency"
          />
        </v-card-text>
        <v-card-text>
          <v-switch
            v-model="switch2"
            inset
            :color="ugcGreen"
            label="Demand Flex"
            @click="toggleFlex"
          />
        </v-card-text>
        <v-card-text>
          <p class="ui__title">
            Metrics
          </p>
          <v-select
            :item-color="ugcGreen"
            :color="ugcGreen"
            :items="metrics"
            label="Metric"
            outlined
          />
        </v-card-text>
      </v-app>
    </div>
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
    value: 0,
    electrification: 0,
    ticksLabels: [
      '0%',
      '25%',
      '50%',
      '75%',
      '100%'
    ],
    layerIds: ['shape-area', 'district'],
    metrics: ['Foo', 'Bar', 'Fizz', 'Buzz'],
    switch1: true,
    switch2: true
  }),
  mounted () {
    this.map.on('load', () => { this.map.setLayoutProperty(this.layerIds[0], 'visibility', 'visible') })
    this.map.on('load', () => { this.map.setLayoutProperty(this.layerIds[1], 'visibility', 'visible') })
  },
  methods: {
    toggleEfficiency () {
      const visibility = this.map.getLayoutProperty(
        this.layerIds[0],
        'visibility'
      )

      // Toggle layer visibility by changing the layout object's visibility property.
      if (visibility === 'visible') {
        this.map.setLayoutProperty(this.layerIds[0], 'visibility', 'none')
        this.className = ''
        this.switch1 = false
      } else {
        this.switch1 = true
        this.className = 'active'
        this.map.setLayoutProperty(
          this.layerIds[0],
          'visibility',
          'visible'
        )
      }
    },
    toggleFlex () {
      const visibility = this.map.getLayoutProperty(
        this.layerIds[1],
        'visibility'
      )

      // Toggle layer visibility by changing the layout object's visibility property.
      if (visibility === 'visible') {
        this.map.setLayoutProperty(this.layerIds[1], 'visibility', 'none')
        this.className = ''
        this.switch2 = false
      } else {
        this.switch2 = true
        this.className = 'active'
        this.map.setLayoutProperty(
          this.layerIds[1],
          'visibility',
          'visible'
        )
      }
    },
    onChildClick (value) {
      // this.fromChild = value
      if (this.ticksLabels[value] === '0%') {
        return this.map.flyTo({
          center: [
            -73.920811, 40.743684
          ],
          bearing: 102,
          pitch: 60,
          zoom: 11,
          essential: true // this animation is considered essential with respect to prefers-reduced-motion
        })
      }
      if (this.ticksLabels[value] === '25%') {
        return this.map.flyTo({
          center: [
            -73.920811, 40.743684
          ],
          bearing: 140,
          pitch: 60,
          zoom: 11,
          essential: true // this animation is considered essential with respect to prefers-reduced-motion
        })
      }
      if (this.ticksLabels[value] === '50%') {
        return this.map.flyTo({
          center: [
            -73.920811, 40.743684
          ],
          bearing: -50,
          pitch: 60,
          zoom: 11,
          essential: true // this animation is considered essential with respect to prefers-reduced-motion
        })
      }
      if (this.ticksLabels[value] === '75%') {
        return this.map.flyTo({
          center: [
            -73.920811, 40.743684
          ],
          bearing: -100,
          pitch: 60,
          zoom: 11,
          essential: true // this animation is considered essential with respect to prefers-reduced-motion
        })
      }
      if (this.ticksLabels[value] === '100%') {
        return this.map.flyTo({
          center: [
            -73.920811,
            40.743684
          ],
          bearing: -150,
          pitch: 60,
          zoom: 11,
          essential: true // this animation is considered essential with respect to prefers-reduced-motion
        })
      }
    }
  }
}
</script>
<style scoped>
  .v-card__text{
    padding:0px !important;
  }
  /* .primary {
    background-color: red;
    border-color: red;
  } */
</style>
