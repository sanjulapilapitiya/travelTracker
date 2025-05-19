<template>
    <div id="app">
      <h1>Travel Tracker</h1>
      <div class="container">
        <div style="padding-bottom: 25px;">
          <Map :locations="locations" @marker-selected="onMarkerSelected" />
        </div>
        <hr>
        <div v-if="locations = selectedLocation">
          <pulse-loader :loading="isLoading" color="white" :size="size" style="padding-top: 10px;"/>
          <div v-show="!isLoading">
            <div class="location-details">
              <h2> {{ selectedLocation.name }} </h2>
              <p style="color: white;">{{ selectedLocation.description }}</p>
            </div>
            <div>
              <div v-if="selectedLocation.insta" class="embed-container">
                <InstagramEmbed :embedUrl="selectedLocation.insta" @loading="isLoading = true" @loaded="isLoading = false"/>
              </div>
            </div>
          </div>
        </div>
      </div>
  </div>
  </template>

<script>
  import { ref } from 'vue';
  import Map from './map.vue';
  import InstagramEmbed from './instagramEmbed.vue';
  import PulseLoader from 'vue-spinner/src/PulseLoader.vue'

  export default {
    name: 'App',
    components: {
      Map,
      InstagramEmbed,
      PulseLoader
    },
    data() {
      return {
        isLoading: false
      };
    },
    setup() {
        // Backend not supported on github pages so using hardcoded data, preferably this would be a backend call
        const locations = ref([
            { lat: 54.535868, lng: -2.152434, name: 'England', description: 'lived here for nearly my entire life, here are my highlights pics:', insta: "" },
            { lat: 48.8566, lng: 2.3522, name: 'France', description: 'just across the pond from where I live, been here a couple times. ignited my passion for traveling as one of the first countries I went to where I have not lived in', insta: "" },
            { lat: 52.34061, lng: -3.28162, name: 'Wales', description: 'will always look fondly from our trips to Wales its my first trip with my partner.', insta: "https://www.instagram.com/p/BsGRLthDBKk/?utm_source=ig_embed&amp;utm_campaign=loading" },
            { lat: 54.58333, lng: -5.93333, name: 'Northern Ireland', description: 'went here for a job interview so only had a couple hours to explore the country! need to go back and explore as it deserves!', insta: "" },
            { lat: 52.52437, lng: 13.41053, name: 'Germany', description: 'was a one of our stops in our inter-railing trip before heading off to Uni', insta: "https://www.instagram.com/p/Bk7Ytl2BnvW/?utm_source=ig_embed&amp;utm_campaign=loading" },
            { lat: 47.49801, lng: 19.03991, name: 'Hungary', description: 'was a one of our stops in our inter-railing trip before heading off to Uni', insta: "https://www.instagram.com/p/Bkrh-vqFOW-/?utm_source=ig_embed&amp;utm_campaign=loading" },
            { lat: 48.20849, lng: 16.37208, name: 'Austria', description: 'was a one of our stops in our inter-railing trip before heading off to Uni', insta: "https://www.instagram.com/p/Bkj5YtplYK4/?utm_source=ig_embed&amp;utm_campaign=loading" },
            { lat: 41.89193, lng: 12.51133, name: 'Italy', description: 'was a one of our stops in our inter-railing trip before heading off to Uni', insta: "https://www.instagram.com/p/BkbIOfBFRfc/?utm_source=ig_embed&amp;utm_campaign=loading" },
            { lat: 52.37403, lng: 4.88969, name: 'Netherlands', description: 'was a one of our stops in our inter-railing trip before heading off to Uni but also the place where I was born so knew the place fairly well', insta: "https://www.instagram.com/p/BlC-FIzBtNz/?utm_source=ig_embed&amp;utm_campaign=loading" },
            { lat: 59.33258, lng: 18.0649, name: 'Sweden', description: 'a long weekend trip with my partner and friends, was very snowy and there was an infinite train ride (long story)', insta: "" },
            { lat: 55.67594, lng: 12.56553, name: 'Denmark', description: 'a long weekend trip with my partner and friends, and a loverly rainbow walkway', insta: "https://www.instagram.com/p/CeMqnpoD8tk/?utm_source=ig_embed&amp;utm_campaign=loading" },
            { lat: 64.13548, lng: -21.89541, name: 'Iceland', description: 'the most beautiful country I have ever been to and the place I got engaged. Oh! also saw the northern lights', insta: "https://www.instagram.com/p/Bdk_4a5FtLz/?utm_source=ig_embed&amp;utm_campaign=loading" },
            { lat: 41.38879, lng: 2.15899, name: 'Spain', description: 'the place where I saw my favorite artist (the weeknd)', insta: "https://www.instagram.com/p/CbkcekmDn6u/?utm_source=ig_embed&amp;utm_campaign=loading" },
            { lat: 38.75382, lng: -9.23083, name: 'Portugal', description: 'favorite holiday I been to with my family had a lovely spot with a pool which came in clutch with the heat (was 40 degrees)', insta: "https://www.instagram.com/p/C4-9sHcirIt/?utm_source=ig_embed&amp;utm_campaign=loading" },
            { lat: 37.97945, lng: 23.71622, name: 'Greece', description: 'been here a couple times best cheese pizza (even beat Italy)', insta: "https://www.instagram.com/p/Blvnh8MlX5U/?utm_source=ig_embed&amp;utm_campaign=loading" },
            { lat: 50.08804, lng: 14.42076, name: 'Czech Republic', description: 'was a one of our stops in our inter-railing trip before heading off to Uni', insta: "https://www.instagram.com/p/Bk0F87GFssv/?utm_source=ig_embed&amp;utm_campaign=loading" },
            { lat: 46.20222, lng: 8.14569, name: 'Switzerland', description: 'birthday present my partner got me, got the famous red train through the alps. it was mind blowing!', insta: "https://www.instagram.com/p/DA040G_CNJS/?utm_source=ig_embed&amp;utm_campaign=loading" },
            { lat: 41.90236, lng: 12.45332, name: 'Vatican City', description: 'was a one of our stops in our inter-railing trip before heading off to Uni', insta: "" },
            { lat: 30.06263, lng: 31.24967, name: 'Egypt', description: 'my best friends dad lived here as a teacher so went with my friend to visit him + have a free place to stay! learnt how to haggle like a pro', insta: "https://www.instagram.com/p/BgjRlt5FJ-R/?utm_source=ig_embed&amp;utm_campaign=loading" },
            { lat: 33.58831, lng: -7.61138, name: 'Morocco', description: 'first holiday with some of my friends (one of which never been abroad). went sand boarding and ate a great deal of sand', insta: "https://www.instagram.com/p/C4ib7c0C92y/?utm_source=ig_embed&amp;utm_campaign=loading" },
            { lat: 6.93194, lng: 79.84778, name: 'Sri Lanka', description: 'lived here a couple years, we holiday here every couple of years to see the family!', insta: "https://www.instagram.com/p/DAF6B_pOahx/?utm_source=ig_embed&amp;utm_campaign=loading" },
            { lat: 3.1412, lng: 101.68653, name: 'Malaysia', description: 'went on a big Asia trip, this was one of the country visited! weirdly this is where my obsession of watches began', insta: "https://www.instagram.com/p/C6970i2SlRt/?utm_source=ig_embed&amp;utm_campaign=loading" },
            { lat: 1.28967, lng: 103.85007, name: 'Singapore', description: 'went on a big Asia trip, this was one of the country visited! best chinese we had!', insta: "https://www.instagram.com/p/C7OLn-Mxgqp/?utm_source=ig_embed&amp;utm_campaign=loading" },
            { lat: -6.21462, lng: 106.84513, name: 'Indonesia', description: 'went on a big Asia trip, this was one of the country visited! was treated like royalty best place to just relax ', insta: "https://www.instagram.com/p/C7pK1VfiNux/?utm_source=ig_embed&amp;utm_campaign=loading" },
            { lat: 34.05223, lng: -118.24368, name: 'America', description: 'went here to visit my partner for her birthday as a surprise whilst she was traveling', insta: "https://www.instagram.com/p/Bv1XQYJDJmE/?utm_source=ig_embed&amp;utm_campaign=loading" },
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
    font-weight: 800;
    font-size: 40px;
    color: white;
}
h2 {
    padding: 25px;
    font-family: 'Papyrus', fantasy;
    font-weight: 900;
    font-size: 30px;
    color: white;
}
#app {
    text-align: center;
    width: 100%;
    height: 100%;
    background: linear-gradient(-45deg, #fefae0, #dda15e, #bc6c25);
    background-size: 400% 400%;
    animation: gradient 30s ease infinite;
    min-height: 100vh;
}
.container {
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
.embed-container {
  float: right;
  padding-right: 10%;
  padding-top: 25px;
  margin: auto;
}
.location-details {
  max-width: 40%;
  padding-left: 10%;
  float: left;
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
  