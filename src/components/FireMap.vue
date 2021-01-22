<template>
  <div class="container">
    <div class="row">
      <div class="title">
        <h2>NASA FIRE MAP</h2>
      </div>
    </div>
    <div>
      <div class="choose">
        <select v-model="presentFilter" style="width:900px">
          <option disabled value="">Please select a day</option>
          <option value="all">Show All</option>
          <option v-for="(fire, index) in filter" :key="index"> {{ fire.date }} </option>
        </select>
      </div>
      <div class="map ">
        <l-map style="height: 87%; width: 100%" :zoom="zoom" :center="center" :minZoom="minZoom">
        <l-tile-layer :url="url"></l-tile-layer>
        <FireMarker v-for="(fire, index) in filteredFires" :key="index" :lat="fire.latitude" :long="fire.longitude" :date="fire.date"/>
      </l-map>
    </div>
  </div>
</div>
</template>

<script>
import { LMap, LTileLayer } from "vue2-leaflet";
import FireMarker from "./Marker";

export default {
  name: "FireMap",
  components: {
    LMap,
    LTileLayer,
    FireMarker,
  },
  props: ["fires"],
  data() {
    return {
      presentFilter: "",
      filteredFires: [],
      url: "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
      zoom: 2,
      center: [41.9109, 12.4818],
      minZoom: 1.5,
    };
  },
  methods: {
    filterByDate() {
      this.filteredFires = [];
      if (this.presentFilter == "all") {
        this.filteredFires = this.filteredFires.concat(this.fires);
      } else {
        this.filteredFires = this.fires.filter(
          (fire) => fire.date == this.presentFilter
        );
      }
    },
  },
  watch: {
    presentFilter() {
      this.filterByDate();
    },
  },
  computed: {
    filter() {
      return [...new Map(this.fires.map((fire) => [fire.date, fire])).values()];
    },
  },
};
</script>
<style>

.choose {
  height: 40px;
  margin-bottom: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.map {
  height: 615px;
  width: 85%;
  margin: 0 auto;
  border-bottom: 2.2px solid #fff;
}

.title {
  display: flex;
  align-items: center;
  justify-content: space-around;
  width: 100%;
  height: 90px;
  margin: 0 auto;
  margin-bottom: 5px;
  margin-top: 15px;
}

.title h2 {
  font-size: 43px;
  text-shadow: 1px 1px 3px #CFCFCF;

}

</style>
