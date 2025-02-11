<template>
    <div id="app">
      <h1>Travel Tracker</h1>
      <div class="map-container">
        <Map :locations="locations" @marker-selected="onMarkerSelected" />
      </div>
      <hr>
      <h2 v-if="locations = selectedLocation">
        {{ selectedLocation.name }}
      </h2>
      <p v-if="selectedLocation?.desciption">{{ selectedLocation.desciption }}</p>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  import Map from './map.vue';
  
  export default {
    name: 'App',
    components: {
      Map,
    },
    setup() {
        // Define an array of locations to display on the map
        const locations = ref([
            { lat: 51.5, lng: -0.09, name: 'England', desciption: 'I live here yo yo yo' },
            { lat: 48.8566, lng: 2.3522, name: 'France' },
            { lat: 53.34061, lng: -1.28162, name: 'Wales' },
            { lat: 54.58333, lng: -5.93333, name: 'Northern Ireland' },
            { lat: 52.52437, lng: 13.41053, name: 'Germany' },
            { lat: 47.49801, lng: 19.03991, name: 'Hungary' },
            { lat: 48.20849, lng: 16.37208, name: 'Austria' },
            { lat: 41.89193, lng: 12.51133, name: 'Italy' },
            { lat: 52.37403, lng: 4.88969, name: 'Netherlands' },
            { lat: 59.33258, lng: 18.0649, name: 'Sweden' },
            { lat: 55.67594, lng: 12.56553, name: 'Denmark' },
            { lat: 64.13548, lng: -21.89541, name: 'Iceland' },
            { lat: 41.38879, lng: 2.15899, name: 'Spain' },
            { lat: 38.75382, lng: -9.23083, name: 'Portugal' },
            { lat: 37.97945, lng: 23.71622, name: 'Greece' },
            { lat: 50.08804, lng: 14.42076, name: 'Czech Republic' },
            { lat: 46.20222, lng: 6.14569, name: 'Switzerland' },
            { lat: 41.90236, lng: 12.45332, name: 'Vatican City' },
            { lat: 30.06263, lng: 31.24967, name: 'Egypt' },
            { lat: 33.58831, lng: -7.61138, name: 'Morocco' },
            { lat: 6.93194, lng: 79.84778, name: 'Sri Lanka' },
            { lat: 3.1412, lng: 101.68653, name: 'Malaysia' },
            { lat: 1.28967, lng: 103.85007, name: 'Singapore' },
            { lat: -6.21462, lng: 106.84513, name: 'Indonesia' },
            { lat: 34.05223, lng: -118.24368, name: 'America' },
        ]);

        const selectedLocation = ref(null);

        const onMarkerSelected = (location) => {
        selectedLocation.value = location;
        };

        return {
            locations,
            selectedLocation,
            onMarkerSelected,
        };
    }
};
</script>
  
<style>
* {
  margin: 0;
  padding: 0; /* reset margin/padding introduced in Import leaflet css in main.js */
}
h1 {
    padding: 25px;
    font-family: 'Papyrus', fantasy;
    font-weight: 900;
    font-size: 40px;
    color: white;
}
#app {
    text-align: center;
    width: 100%;
    background: linear-gradient(-45deg, #fefae0, #dda15e, #bc6c25);
    background-size: 400% 400%;
    animation: gradient 30s ease infinite;
    height: 100vh;
}
.map-container {
    width: 100%;
    max-width: 900px;
    height: 500px;
    padding: 15px;
    margin: 0 auto; /* Center the map container horizontally */
}
hr {
  border: 1px solid #fefae0;
  max-width: 75%;
  text-align: center;
  border-radius: 5px;
  margin: auto;
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
</style>
  