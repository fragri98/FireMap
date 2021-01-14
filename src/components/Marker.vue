<template>
  <div>
    <l-marker :lat-lng="markerLatLng">
      <l-tooltip>Latitude: {{ this.lat }} Longitude: {{ this.long }}
        <br />
        Date: {{ this.date }} </l-tooltip>
    </l-marker>
  </div>
</template>

<script>
/* eslint-disable no-undef */
import { LMarker, LTooltip } from "vue2-leaflet";
import { Icon } from "leaflet";
delete Icon.Default.prototype._getIconUrl;
Icon.Default.mergeOptions({
  iconRetinaUrl: require("leaflet/dist/images/fire_logo.png"),
  iconUrl: require("leaflet/dist/images/fire_logo.png"),
  shadowUrl: require("leaflet/dist/images/marker-shadow.png"),
});
export default {
  name: "FireMarker",
  components: { LMarker, LTooltip },
  props: ["lat", "long", "date"],
  data() {
    return {
      markerLatLng: [this.lat, this.long],
    };
  },
};
</script>

<style></style>
