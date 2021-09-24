<template>
  <div>
    <v-app>
      <div class="ui__left">
        <p class="ui__title__no-rule">
          Congressional District: <span id="features" />
        </p>
        <p class="ui__title__no-rule">
          Congressional District: <span id="features" />
        </p>
        <p class="ui__title__no-rule">
          Congressional District: <span id="features" />
        </p>
        <div class="ui__element">
          <v-card-text>
            <v-tooltip left>
              <template #activator="{ on, attrs }">
                <p
                  v-bind="attrs"
                  class="ui__title"
                  v-on="on"
                >
                  Adoption<v-icon
                    dark
                    right
                  >
                    mdi-help-circle
                  </v-icon>
                </p>
              </template>
              <span style="width: 200px;">Though the "loose" option was set to "false" in your @babel/preset-env config, it will not be used for @babel/plugin-proposal-private-property-in-object since the "loose" mode option was set to "true" for @babel/plugin-proposal-private-methods.</span>
            </v-tooltip>
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
            <v-tooltip left>
              <template #activator="{ on, attrs }">
                <p
                  v-bind="attrs"
                  class="ui__title"
                  v-on="on"
                >
                  Filters<v-icon
                    dark
                    right
                  >
                    mdi-help-circle
                  </v-icon>
                </p>
              </template>
              <span style="width: 200px;">Toggle different filters to see how they effect the metrics.</span>
            </v-tooltip>
            <div
              style="display:flex;"
            >
              <v-switch
                v-model="switch1"
                inset
                :color="ugcGreen"
                label="Energy Efficiency"
                @click="toggleEfficiency"
              />
              <v-tooltip left>
                <template #activator="{ on, attrs }">
                  <v-icon
                    v-bind="attrs"
                    dark
                    right
                    v-on="on"
                  >
                    mdi-help-circle
                  </v-icon>
                </template>
                <span style="width: 200px;">Simple energy efficnecy upgrades like sealing cracks and gaps in the walls, adding insulation to the roofs, installing better lights like LEDs and installing Energy Star appliances and controlling other plug loads like computers are included alongside heat pump instilations.</span>
              </v-tooltip>
            </div>
          </v-card-text>
          <v-card-text>
            <div
              style="display:flex;"
            >
              <v-switch
                v-model="switch2"
                inset
                :color="ugcGreen"
                label="Demand Flexability"
                @click="toggleFlex"
              />
              <v-tooltip left>
                <template #activator="{ on, attrs }">
                  <v-icon
                    v-bind="attrs"
                    dark
                    right
                    v-on="on"
                  >
                    mdi-help-circle
                  </v-icon>
                </template>
                <span style="width: 200px;">Demand flexibility is all about shifting power demand to times when the grid is not stressed. Batteries and thermal storage technologies are included alongside heat pump instillations.</span>
              </v-tooltip>
            </div>
          </v-card-text>
        </div>
      </div>
      <div class="ui__right">
        <div class="ui__element">
          <p class="ui__title__no-rule">
            <v-icon
              style="color:#C0D72D;font-size:16pt;"
              dark
              left
            >
              mdi-texture-box
            </v-icon>Zone
          </p>
          <v-card-text>
            <v-select
              :item-color="ugcGreen"
              :color="ugcGreen"
              :items="metrics"
              label="Zone"
              outlined
            />
          </v-card-text>
          <v-card-text>
            <p class="ui__title">
              <v-icon
                style="color:#C0D72D;font-size:16pt;"
                dark
                left
              >
                mdi-cog-outline
              </v-icon>Metrics
            </p>
            <v-select
              :item-color="ugcGreen"
              :color="ugcGreen"
              :items="metrics"
              label="Metric"
              outlined
              return-object
              @change="getLegend"
            />
          </v-card-text>
          <v-card-text>
            <div class="ui__legend">
              <v-tooltip left>
                <template #activator="{ on, attrs }">
                  <p
                    v-bind="attrs"
                    class="ui__title"
                    v-on="on"
                  >
                    Legend  <v-icon
                      dark
                      right
                    >
                      mdi-help-circle
                    </v-icon>
                  </p>
                </template>
                <span style="width: 200px;">Though the "loose" option was set to "false" in your @babel/preset-env config, it will not be used for @babel/plugin-proposal-private-property-in-object since the "loose" mode option was set to "true" for @babel/plugin-proposal-private-methods.
                  The "loose" option must be the same for @babel/plugin-proposal-class-properties, @babel/plugin-proposal-private-methods and @babel/plugin-proposal-private-property-in-object (when they are enabled): you can silence this warning by explicitly adding
                  ["@babel/plugin-proposal-private-property-in-object", { "loose": true }]
                  to the "plugins" section of your Babel config.</span>
              </v-tooltip>
              <p class="ui__subtitle">
                {{ legend }}
              </p>
              <div v-if="legend == 'Remaining Capacity (%)'" class="ui__legend__marker">
                <div class="ui__legend__remainingCap" />
                <div class="ui__legend__remainingCap" />
                <div class="ui__legend__remainingCap" />
                <div class="ui__legend__remainingCap" />
                <div class="ui__legend__remainingCap" />
                <div class="ui__legend__remainingCap" />
                <div class="ui__legend__remainingCap" />
                <div class="ui__legend__remainingCap" />
                <div class="ui__legend__remainingCap" />
                <div class="ui__legend__remainingCap" />
              </div>
              <div v-if="legend == 'Increase in Demand (MW)'" class="ui__legend__marker">
                <div class="ui__legend__increaseMW" />
                <div class="ui__legend__increaseMW" />
                <div class="ui__legend__increaseMW" />
                <div class="ui__legend__increaseMW" />
                <div class="ui__legend__increaseMW" />
                <div class="ui__legend__increaseMW" />
                <div class="ui__legend__increaseMW" />
                <div class="ui__legend__increaseMW" />
              </div>
            </div>
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
    switch1: true,
    switch2: true,
    legend: ''
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
    getLegend (e) {
      this.legend = e
    },
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
 .v-tooltip__content {
   background-color: black;
   color: white;
   font-family: 'Gotham-book';
  opacity: 0.9 !important;
 width: 250px !important;
 border-radius: 0px !important;
}
.v-icon.v-icon{
  font-size: 16px;
  opacity: .5;
}
</style>
