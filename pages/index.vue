<template>
  <div>
    <Map />
  </div>
</template>

<script>

export default {

  data () {
    return {

    }
  },
  head () {
    return {
      title: 'UGC Grid Impact Study',
      meta: [{
        name: 'Description',
        content: 'Grid Impact Study',
        hid: 'description'
      }],
      link: [
        {
          rel: 'stylesheet',
          href: 'https://api.mapbox.com/mapbox-gl-js/v1.10.0/mapbox-gl.css'
        }
      ]
    }
  }
}
</script>

<style lang="scss">
  @import './styles/index.scss';

</style>
