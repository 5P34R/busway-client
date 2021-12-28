<template>
<button @click="locate">locate</button>
  <div v-if="location">
    <h1>{{ location.latitude}}</h1>
</div>
 
<button @click="filter">Filter</button>

</template>

<script>

import L from 'leaflet';

export default {
  name: "Home",
  components: {},
  data(){
    return {
      location :null,
      distance : 0,
      coo : [
        {lat: '11111', long:'11111'},
        {lat: '22222', long:'22222'},
        {lat: '33333', long:'33333'},
        {lat: '44444', long:'44444'}
      ]
    }
  },

  methods: {
      
    locate(){
       if(navigator.geolocation){
         navigator.geolocation.getCurrentPosition(position => {
           console.log(position.latitude)
           console.log(position.longitude)
          },
         err => {
           console.log(err);
         }
         )
       }else {
         console.log("Your brower doesnt npt support")
       }
       this.calDist();
    },
    calDist(lat1, lon1, lat2, lon2){
      let l1 = L.latLng(lat1, lon1);
      let l2 = L.latLng(lat2,lon2)
      console.log(l1.distanceTo(l2)/ 1000);
    },

    filter(){
      this.coo.forEach(item => {
        this.calDist(this.position.latitude, this.position.longitude, item.lat, item.long)
      });
    }
  }
};
</script>
