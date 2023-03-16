<template>
  <l-map use-global-leaflet ref="map" :zoom="zoom" @ready="onLeafletReady">
    <template v-if="leafletReady">
      <l-tile-layer :url="url" />
    </template>
  </l-map>
</template>
<script>
import "leaflet";

import "leaflet/dist/leaflet.css";
import "leaflet-draw/dist/leaflet.draw.css";
import "leaflet-toolbar/dist/leaflet.toolbar.css";

import { LMap, LGeoJson, LTileLayer } from "@vue-leaflet/vue-leaflet";

import "leaflet-draw/dist/leaflet.draw-src.js";
import "leaflet-toolbar";
import "leaflet-draw-toolbar/dist/leaflet.draw-toolbar.js";

export default {
  components: {
    LMap,
    LTileLayer,
    LGeoJson,
  },

  data() {
    return {
      url: "https://{s}.tile.osm.org/{z}/{x}/{y}.png",
      zoom: 1,

      leafletReady: false,
      leafletObject: null,

      visible: false,
    };
  },

  methods: {
    async onLeafletReady() {
      await this.$nextTick();
      this.leafletObject = this.$refs.map.leafletObject;
      this.leafletReady = true;

      new L.Toolbar2.DrawToolbar({
        position: "topleft",
      }).addTo(this.leafletObject);
    },
  },
};
</script>
