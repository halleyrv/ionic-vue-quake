<template>

<ion-app>
  <ion-header>
    <ion-toolbar color="primary">
      <ion-title>App</ion-title>
    </ion-toolbar>
  </ion-header>

  <ion-content class="ion-padding">
     <QuakeMap />
  </ion-content>
</ion-app>
  
</template>

<script>
// @ is an alias to /src
import QuakeMap from '@/components/QuakeMap.vue'

export default {
  name: 'Home',
  components: {
    QuakeMap
  }
}
</script>
