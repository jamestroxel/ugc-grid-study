<template>
  <div>
    <div class="map__wrapper" />
    <Ui :map="map" />
    <div id="map" class="dark" />
  </div>
</template>

<script>
import mapboxgl from 'mapbox-gl'
export default {
  data () {
    return {
      map: {},
      switch1: false
    }
  },
  mounted () {
    this.createMap()
  },
  methods: {
    createMap () {
      mapboxgl.accessToken = 'pk.eyJ1IjoiamFtZXN0cm94ZWwiLCJhIjoiY2tzMjk0dGx0MTRsMjJ1cndsNDF4a3BmdCJ9.gk2m893L7akKBdyE3RAK1A'
      this.map = new mapboxgl.Map({
        container: 'map',
        style: 'mapbox://styles/jamestroxel/ckteyjs3k10gr17p61exf9uju',
        center: [-73.989, 40.713],
        bearing: 0,
        pitch: 0,
        zoom: 10.5
        // attributionControl: false
      })
    }
  }
}

</script>
