<template>
    <div ref="embedContainer">
      <blockquote
        class="instagram-media"
        :data-instgrm-permalink="embedUrl"
        data-instgrm-version="14"
      ></blockquote>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      embedUrl: {
        type: String,
        required: true
      }
    },
    mounted() {
      this.loadInstagramScript();
      console.log(this.embedUrl);
    },
    methods: {
      loadInstagramScript() {
        // Check if the Instagram script is already loaded
        if (!document.getElementById('instagram-embed-script')) {
          const script = document.createElement('script');
          script.id = 'instagram-embed-script';
          script.src = 'https://www.instagram.com/embed.js';
          script.async = true;
          script.onload = this.processEmbeds;
          document.body.appendChild(script);
        } else {
          this.processEmbeds();
        }
      },
      processEmbeds() {
        // Ensure Instagram embed processing happens after the script is loaded
        window.instgrm?.Embeds?.process();
      }
    }
  };
  </script>
  
  