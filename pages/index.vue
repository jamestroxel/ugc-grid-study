<template>
  <div>
    <Map />
    <div class="footer__wrapper">
      <div class="footer__content" />
    </div>
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
  .v-application{
    background:transparent !important;
    font-family: 'Gotham Book';
  }
  .v-application ul{
    padding-left: 0px;
  }
  .mapboxgl-ctrl.mapboxgl-ctrl-attrib{
    background-color: transparent !important;
  }
  .mapboxgl-ctrl-attrib a{
    color:white !important;
  }
  .v-input{
    font-size: 14px !important;
    line-height: 2 !important;
  }
  // .v-label{
  //   font-size: 1.6rem !important;
  //   line-height: 1.5 !important;
  // }
</style>
