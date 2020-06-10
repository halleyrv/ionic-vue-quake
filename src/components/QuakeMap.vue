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
        :icon="m.icon"
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
      sismos: []
    };
  },

  mounted() {
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
            lng: element.longitude,
            icon: this.getColorMagnitude(element.magnitude)
          };
          this.markers.push({ position: marker ,icon: marker.icon});
        });
      } catch (error) {
        console.log(error)
      }
      
    
    },
    getColorMagnitude(magnitude){
      let icon ="http://maps.google.com/mapfiles/ms/icons/"
      switch (true) {
        case (magnitude<=4):
          icon = icon+  "green-dot.png" 
          break;
        case (magnitude <=6):
          icon = icon+  "yellow-dot.png" 
          break;
        default:
          icon = icon + "red-dot.png"
          break;
      }
     return icon
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
