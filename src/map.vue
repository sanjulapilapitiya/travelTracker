<template>
    <div id="map" style="height: 500px;"></div>
  </template>
  
  <script>
  import { onMounted } from 'vue'; // Import the Vue 3 lifecycle hook
  import L from 'leaflet'; // Import Leaflet
  
  export default {
    name: 'Map',
    props: {
        locations: Array,
    },
    emits: ['marker-selected'],
    setup(props, { emit }) {
      onMounted(() => {
        console.log(props.locations);
        // Fix for missing marker icons
        delete L.Icon.Default.prototype._getIconUrl;

        L.Icon.Default.mergeOptions({
        iconUrl: 'https://unpkg.com/leaflet@1.7.1/dist/images/marker-icon.png',
        iconRetinaUrl: 'https://unpkg.com/leaflet@1.7.1/dist/images/marker-icon-2x.png',
        shadowUrl: 'https://unpkg.com/leaflet@1.7.1/dist/images/marker-shadow.png'
        });

        // Initialize the map
        const map = L.map('map').setView([51.505, -0.09], 2); // Set the initial view (latitude, longitude, zoom level)
  
        L.tileLayer('https://tiles.stadiamaps.com/tiles/stamen_watercolor/{z}/{x}/{y}.jpg', {
            attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, ' +
                        '&copy; <a href="https://stadia.maps.io">Stadia Maps</a>, ' +
                        '&copy; <a href="http://stamen.com">Stamen Design</a>',
            maxZoom: 18
        }).addTo(map);

        const customIcon = L.icon({
            iconUrl: '/asset/pin.png',
            iconSize: [20, 20],
        });
  
        // Add markers to the map for each location
        props.locations.forEach((location) => {
          L.marker([location.lat, location.lng], { icon: customIcon }).addTo(map)
            .bindPopup(`<b>${location.name}</b>`)
            .on('click', () => {
                emit('marker-selected', location);
            });
        });
      });
    },
  };
  </script>
  