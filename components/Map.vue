<template>
  <div>
    <div class="map__wrapper">
      <div id="map" class="dark" />
    </div>
    <Slider @childToParent="onChildClick" />
  </div>
</template>

<script>

import mapboxgl from 'mapbox-gl'
export default {
  data () {
    return {
      map: {},
      fromChild: ''
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
        style: 'mapbox://styles/jamestroxel/cks264k5p96qv18rzz44xe490',
        center: [-74.5,
          40],
        bearing: 102,
        pitch: 75,
        zoom: 11,
        attributionControl: false
      })
    },
    // mapView () {
    //   if (this.fromChild === '0%') {
    //     this.map.flyTo({
    //       center: [
    //         -74.5 + (Math.random() - 0.5) * 10,
    //         40 + (Math.random() - 0.5) * 10
    //       ],
    //       essential: true // this animation is considered essential with respect to prefers-reduced-motion
    //     })
    //   }
    //   if (this.fromChild === '25%') {
    //     this.map.flyTo({
    //       center: [
    //         -75.5 + (Math.random() - 0.5) * 10,
    //         40 + (Math.random() - 0.5) * 10
    //       ],
    //       essential: true // this animation is considered essential with respect to prefers-reduced-motion
    //     })
    //   }
    // },
    onChildClick (value) {
      // this.fromChild = value
      if (value === '0%') {
        return this.map.flyTo({
          center: [
            -74.5,
            40
          ],
          bearing: 102,
          pitch: 75,
          zoom: 11,
          essential: true // this animation is considered essential with respect to prefers-reduced-motion
        })
      }
      if (value === '25%') {
        return this.map.flyTo({
          center: [
            -74.5,
            40
          ],
          bearing: 140,
          pitch: 75,
          zoom: 11,
          essential: true // this animation is considered essential with respect to prefers-reduced-motion
        })
      }
      if (value === '50%') {
        return this.map.flyTo({
          center: [
            -74.5,
            40
          ],
          bearing: -50,
          pitch: 75,
          zoom: 11,
          essential: true // this animation is considered essential with respect to prefers-reduced-motion
        })
      }
      if (value === '75%') {
        return this.map.flyTo({
          center: [
            -74.5,
            40
          ],
          bearing: -100,
          pitch: 75,
          zoom: 11,
          essential: true // this animation is considered essential with respect to prefers-reduced-motion
        })
      }
      if (value === '100%') {
        return this.map.flyTo({
          center: [
            -74.5,
            40
          ],
          bearing: -150,
          pitch: 75,
          zoom: 11,
          essential: true // this animation is considered essential with respect to prefers-reduced-motion
        })
      }
    }
  }
}

</script>
