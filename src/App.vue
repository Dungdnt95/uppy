<template>
  <div class="form-group">
    <p id="browse" class="upload-msg mb-0">vãi</p>
    <!-- <button id="browse">Select Files</button> -->
  </div>
</template>

<script>

import Uppy from "@uppy/core";
import Dashboard from "@uppy/dashboard";
import RemoteSources from "@uppy/remote-sources";
import { COMPANION_URL, COMPANION_ALLOWED_HOSTS } from "@uppy/transloadit";
import "@uppy/core/dist/style.css";
import "@uppy/dashboard/dist/style.css";
import Tus from "@uppy/tus";

export default {
  props: {
    maxFileSizeInBytes: {
      type: Number,
      required: true,
    },
  },

  data() {
    return {
      payload: null,
      previewPath: null,
      disabled: true,
      url: "",
      COMPANION_URL: "http://companion.uppy.io",
      COMPANION_ALLOWED_HOSTS: ["https://my-site.com"],
    };
  },
  mounted() {
    this.instantiateUppy();
  },
  methods: {
    instantiateUppy() {
      this.uppy = new Uppy()
        .use(Dashboard, { trigger: "#browse" })
        .use(RemoteSources, {
          companionUrl: "http://companion.uppy.io",
          sources: ["Instagram", "GoogleDrive"],
          companionAllowedHosts: ["https://my-site.com"],
        })
        .use(Tus, { endpoint: "https://tusd.tusdemo.net/files/" })
        .on("complete", ({ transloadit }) => {})
        .on("error", (error) => {
          console.error(error);
        });
    },
  },
};
</script>

<style scoped>
.image-container {
  height: 150px;
  width: 150px;
  border-radius: 50%;
  overflow: hidden;
  margin-right: auto;
  margin-left: auto;
}

.image-container > img {
  width: inherit;
  height: inherit;
}
</style>
