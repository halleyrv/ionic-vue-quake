<template>
  <div class="hello">
    <h1>Terremotos</h1>
    <gmap-map
      :center="center"
      :zoom="5"
      style="width:100%;  height: 600px;"
    >
      <gmap-marker
        :key="index"
        v-for="(m, index) in markers"
        :position="m.position"
        @click="center=m.position"
      ></gmap-marker>
    </gmap-map>
  </div>
</template>

<script>
export default {
  name: 'QuakeMap',
    data() {
    return {

      center: { lat: -35.675148, lng: -71.5429688 },
      markers: [],
      places: [],
      sismos: [],
      currentPlace: null
    };
  },

  mounted() {
    //this.geolocate();
    this.loadMarkers();
  },

  methods: {
   
     async loadMarkers(){
      let url_endpoint = "https://chilealerta.com/api/query/?user=demo&select=ultimos_sismos"
      
      try {
         const { data } = await this.axios.get(url_endpoint)
         
          this.sismos = data.ultimos_sismos
    
          this.sismos.forEach(element => {
          const marker = {
            lat: element.latitude,
            lng: element.longitude
          };
          this.markers.push({ position: marker });
        });
      } catch (error) {
        console.log(error)
      }
      
    
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
