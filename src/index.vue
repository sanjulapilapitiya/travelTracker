<template>
    <div id="app">
      <h1>Travel Tracker</h1>
      <div class="map-container">
        <Map />
      </div>
    </div>
  </template>
  
  <script>
  import Map from './map.vue';
  
  export default {
    name: 'App',
    components: {
      Map,
    },
  };
</script>
  
<style>
* {
  margin: 0;
  padding: 0; /* reset margin/padding introduced in Import leaflet css in main.js */
}
#app {
    text-align: center;
    width: 100%;
    background: linear-gradient(-45deg, #606c38, #283618,#fefae0, #dda15e, #bc6c25);
    background-size: 400% 400%;
    animation: gradient 30s ease infinite;
    height: 100vh;
}
@keyframes gradient {
    0% {
        background-position: 0% 50%;
    }
 
    50% {
        background-position: 100% 50%;
    }
 
    100% {
        background-position: 0% 50%;
    }
}
.map-container {
    width: 100%;
    max-width: 900px;
    height: 500px;
    margin: 0 auto; /* Center the map container horizontally */
}
</style>
  