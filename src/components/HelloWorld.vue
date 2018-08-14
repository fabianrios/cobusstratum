<template>
  <div class="hello">
    <Menu :links="obj" :selected="selected" />
    <div id="map"></div>
  </div>
</template>

<script>
import mapboxgl from 'mapbox-gl'
import Menu from '@/components/Menu'

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'New York',
      selected: this.$route.params.where || 'newyork',
      obj: {
        'newyork': {
          name: 'New York',
          coord: {
            lat: 40.7128,
            lng: -74.0060
          }
        },
        'moscow': {
          name: 'Moscow',
          coord: {
            lat: 55.7558,
            lng: 37.6173
          }
        },
        'bogota': {
          name: 'Bogotá',
          coord: {
            lat: 4.7110,
            lng: -74.0721
          }
        },
        'berlin': {
          name: 'Berlin',
          coord: {
            lat: 52.5200,
            lng: 13.4050
          }
        },
        'shangai': {
          name: 'Shangai',
          coord: {
            lat: 31.2304,
            lng: 121.4737
          }
        }
      },
      token: process.env.TOKEN
    }
  },
  mounted () {
    this.createMap()
  },
  methods: {
    createMap: function () {
      let geojson = [{
        'type': 'Feature',
        'geometry': {
          'type': 'Point',
          'coordinates': [this.obj[this.selected].coord.lng, this.obj[this.selected].coord.lat]
        },
        'properties': {
          'title': '1',
          'icon': 'monument'
        }
      }, {
        'type': 'Feature',
        'geometry': {
          'type': 'Point',
          'coordinates': [this.obj[this.selected].coord.lng, 40.776]
        },
        'properties': {
          'title': '2',
          'icon': 'harbor'
        }
      }]
      mapboxgl.accessToken = this.token
      // init the map
      this.map = new mapboxgl.Map({
        style: 'mapbox://styles/mapbox/light-v9',
        center: [this.obj[this.selected].coord.lng, this.obj[this.selected].coord.lat],
        zoom: 10,
        container: 'map'
      }).on('load', function () {
        this.addLayer({
          'id': 'points',
          'type': 'symbol',
          'source': {
            'type': 'geojson',
            'data': {
              'type': 'FeatureCollection',
              'features': geojson
            }
          },
          'layout': {
            'icon-image': '{icon}-15',
            'text-field': '{title}',
            'text-font': ['Open Sans Semibold', 'Arial Unicode MS Bold'],
            'text-offset': [0, 0.6],
            'text-anchor': 'top'
          }
        })
      })
    }
  },
  components: {
    Menu
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
</style>
