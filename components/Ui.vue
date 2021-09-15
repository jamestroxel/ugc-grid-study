<template>
  <div>
    <nav class="navigation">
      <ul class="navigation__list">
        <li class="navigation__list__item">
          <nuxt-link to="/" class="navigation__list__link">
            <svg id="Layer_1" style="z-index:300;" data-name="Layer 1" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 150 149.54"><defs><style>.cls-1{fill:#fff;}</style></defs><polygon class="cls-1" points="17.8 0 17.8 64.02 8.79 64.02 8.79 0 0 0 0 72.81 26.59 72.81 26.59 0 17.8 0" /><path class="cls-1" d="M70.7,32.57V0H61.9V72.81H88.34V32.57ZM79.55,64H70.7V41.36h8.85Z" /><path class="cls-1" d="M92.74,0V8.79H110.3V32.57H92.74V72.81H119.1V0ZM110.3,64h-8.77V41.36h8.77Z" /><polygon class="cls-1" points="123.49 0 123.49 72.81 132.28 72.81 132.28 8.79 141.21 8.79 141.21 72.81 150 72.81 150 0 123.49 0" /><path class="cls-1" d="M0,77.21V118H17.8v22.75H0v8.79H26.59V77.21ZM8.79,86h9v23.17h-9Z" /><path class="cls-1" d="M88.34,118V77.2H61.9v72.3H88.34v-8.79H70.7V118ZM70.7,86h8.85v23.17H70.7Z" /><path class="cls-1" d="M119.1,118V77.2H92.74v72.3H119.1v-8.79H101.53V118ZM101.53,86h8.77v23.17h-8.77Z" /><polygon class="cls-1" points="123.49 149.5 132.28 149.5 132.28 86 141.21 86 141.21 149.5 150 149.5 150 77.2 123.49 77.2 123.49 149.5" /><polygon class="cls-1" points="57.51 32.56 57.51 0 30.99 0 30.99 72.81 39.78 72.81 39.78 8.79 48.72 8.79 48.72 32.56 57.51 32.56" /><polygon class="cls-1" points="57.51 109.15 57.51 77.2 30.99 77.2 30.99 149.5 39.78 149.5 39.78 86 48.72 86 48.72 109.15 57.51 109.15" /></svg>
            <p class="navigation__title">
              NYC Grid<br> Impact Tool
            </p>
          </nuxt-link>
        </li>
        <li class="navigation__list__item">
          <nuxt-link to="/" class="navigation__list__link">
            <p>
              About
            </p>
          </nuxt-link>
        </li>
      </ul>
    </nav>
    <nuxt />
    <v-app>
      <div class="ui__analysis__wrapper">
        <div class="ui__analysis__item">
          <v-select
            :item-color="ugcGreen"
            :color="ugcGreen"
            :items="analysis"
            label="Analysis"
            outlined
          />
        </div>
      </div>
      <div class="ui__wrapper">
        <p class="ui__title">
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
    analysis: ['User-Guided', 'Featured Analysis'],
    switch1: true,
    switch2: true
  }),
  mounted () {
    this.map.on('load', () => { this.map.setLayoutProperty(this.layerIds[0], 'visibility', 'visible') })
    this.map.on('load', () => { this.map.setLayoutProperty(this.layerIds[1], 'visibility', 'visible') })
    this.map.on('mousemove', (e) => {
      const features = this.map.queryRenderedFeatures(e.point)

      // Limit the number of properties we're displaying for
      // legibility and performance
      // const displayProperties = [
      //   'type',
      //   'properties'
      //   // 'id',
      //   // 'layer',
      //   // 'source',
      //   // 'sourceLayer',
      //   // 'state'
      // ]

      // const displayFeatures = features.map((feat) => {
      //   const displayFeat = {}
      //   displayProperties.forEach((prop) => {
      //     displayFeat[prop] = feat[prop]
      //   })
      console.log(features[0].properties.CongDist)
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
