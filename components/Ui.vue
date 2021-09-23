<template>
  <div>
    <v-app>
      <div class="ui__left">
        <p class="ui__vizBox__title">
          Congressional District: <span id="features" />
        </p>
        <div class="ui__element">
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
        </div>
      </div>
      <div class="ui__right">
        <p class="ui__vizBox__title">
          Congressional District: <span id="features" />
        </p>
        <div class="ui__element">
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
              dense
            />
          </v-card-text>
          <div class="ui__legend">
          </div>
        </div>
      </div>
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
    metrics: ['Remaining Capacity (%)', 'Increase in Demand (MW)', 'Increase in Demand (%)', 'Summer vs. Winter Peak'],
    switch1: true,
    switch2: true
  }),
  mounted () {
    this.map.on('load', () => { this.map.setLayoutProperty(this.layerIds[0], 'visibility', 'visible') })
    this.map.on('load', () => { this.map.setLayoutProperty(this.layerIds[1], 'visibility', 'visible') })
    this.map.on('mousemove', (e) => {
      const features = this.map.queryRenderedFeatures(e.point)
      if (!features[0].properties.CongDist) {
        return ''
      } else {
        document.getElementById('features').innerHTML = JSON.stringify(
          features[0].properties.CongDist,
          null,
          2
        )
      }

      // Write object as string with an indent of two spaces.
    })
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
  #features{
    font-family: 'gotham-book';
  }
  /* .primary {
    background-color: red;
    border-color: red;
  } */
</style>
