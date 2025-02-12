<template>
  <div ref="embedContainer"></div>
</template>

<script>
import { nextTick } from "vue";

export default {
  props: {
    embedUrl: {
      type: String,
      required: true
    }
  },
  emits: ["loading", "loaded"],
  watch: {
    embedUrl: {
      immediate: true,
      handler() {
        this.loadInstagramEmbed();
      }
    }
  },
  methods: {
    async loadInstagramEmbed() {
      // Emit "loading" event to notify parent component
      this.$emit("loading");

      // Wait for the DOM to render
      await nextTick();

      if (this.$refs.embedContainer) {
        this.$refs.embedContainer.innerHTML = `<blockquote class="instagram-media" data-instgrm-permalink="${this.embedUrl}" data-instgrm-version="14"></blockquote>`;

        // Dynamically load or reprocess the Instagram embed script
        if (!window.instgrm) {
          const script = document.createElement("script");
          script.src = "https://www.instagram.com/embed.js";
          script.async = true;
          script.onload = () => {
            window.instgrm.Embeds.process();
          };
          document.body.appendChild(script);
        } else {
          window.instgrm.Embeds.process();
        }
        setTimeout(() => {
        this.$emit("loaded");
      }, 1000); // set a 1 secs timer as instagram on average take a that long to render
      }
    }
  }
};
</script>
