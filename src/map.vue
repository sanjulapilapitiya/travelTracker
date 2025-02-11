<template>
    <div id="map" style="height: 500px;"></div>
  </template>
  
  <script>
  import { onMounted } from 'vue'; // Import the Vue 3 lifecycle hook
  import L from 'leaflet'; // Import Leaflet
  
  export default {
    name: 'Map',
    setup() {
      onMounted(() => {
        // Fix for missing marker icons
        delete L.Icon.Default.prototype._getIconUrl;

        L.Icon.Default.mergeOptions({
        iconUrl: 'https://unpkg.com/leaflet@1.7.1/dist/images/marker-icon.png',
        iconRetinaUrl: 'https://unpkg.com/leaflet@1.7.1/dist/images/marker-icon-2x.png',
        shadowUrl: 'https://unpkg.com/leaflet@1.7.1/dist/images/marker-shadow.png'
        });

        // Initialize the map
        const map = L.map('map').setView([51.505, -0.09], 2); // Set the initial view (latitude, longitude, zoom level)
  
        // Add OpenStreetMap tile layer (OSM tiles)
        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
          attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
        }).addTo(map);
  
        // Define an array of locations to display on the map
        const locations = [
          { lat: 51.5, lng: -0.09, name: 'England' },
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
        ];
  
        // Add markers to the map for each location
        locations.forEach((location) => {
          L.marker([location.lat, location.lng]).addTo(map)
            .bindPopup(`<b>${location.name}</b>`);
        });
      });
    },
  };
  </script>
  