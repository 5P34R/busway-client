1
<template>
<button @click="locate">locate</button>
  <div v-if="location">
    <h1>{{ location.latitude}}</h1>
</div>
 
<button @click="filter">Filter</button>
<button @click="loadData">locate</button>
</template>

<script>

import L from 'leaflet';
import axios from 'axios';
export default {
  name: "Home",
  components: {},
  data(){
    return {
      location :null,
      distance : 0,
      corrs : [
        {lat: '111111', lon: '11111'},
        {lat: '222222', lon: '22222'},
        {lat: '333333', lon: '33333'},
        {lat: '444444', lon: '44444'},
      ]
    }
  },

  methods: {
    async loadData(){
      var data = await axios.get('http://athul.local:8000/api/method/get_bus_timings')
      console.log(data)
    },
      
    locate(){
       if(navigator.geolocation){
         navigator.geolocation.getCurrentPosition(position => {
           console.log(position)
          this.location = position.coords
          },
         err => {
           console.log(err);
         }
         )
       }else {
         console.log("Your brower doesnt npt support")
       }
       
    },
    calDist(lat1, lon1, lat2, lon2){
      let l1 = L.latLng(lat1, lon1);
      let l2 = L.latLng(lat2,lon2)
      console.log(l1.distanceTo(l2)/ 1000);
    },
    filter(){

    }
  }
};
</script>
