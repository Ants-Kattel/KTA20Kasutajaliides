<template>
<div>
  <v-btn @click="center={lat: 59.42534259402756, lng:24.74422244589635}; zoom=18">go to somewhere</v-btn>
  <v-btn @click="locations.push([getRandomArbitrary(-90,90), getRandomArbitrary(-180, 180)])">Add random marker</v-btn>
  <v-btn @click="locations.pop()">Remove last marker</v-btn>
  <google-map :center="center" :zoom="zoom" :locations="locations"></google-map>
</div>
</template>

<script>
import GoogleMap from '~/components/GoogleMap.vue'

export default {
  components: { GoogleMap },
  methods: {
    getRandomArbitrary(min, max) {
      return Math.random() * (max - min) + min;
    },
  },
  data(){
      return {
          center: {lat: 44, lng: 24},
          zoom: 4,
          locations: [[36.34468401811695, 138.65080643325922],[36.28795903272529, 138.75427678332], [36.48310120921732, 138.89644946209842],[36.52743782398204, 139.15176852219983], [36.7394491866612, 139.52614924373523], [36.92181825838466, 139.82448618297562]]
         
      }
  },

}
</script>

<style>
   
</style>