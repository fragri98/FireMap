<template>
  <div id="app">
    <FireMap :fires="firesDataList" /> <br/>
    <FooterMap/>
  </div>

</template>

<script>
import FireMap from "./components/FireMap.vue";
import FooterMap from "./components/Footer.vue";


export default {
  name: "App",
  data() {
    return {
      firesDataList: [],
    };
  },
  components: {
    FireMap,
    FooterMap,
  },
  mounted: async function() {
    const response = await fetch(
      "https://d1sat59n3r2spx.cloudfront.net/static/s2impact-global-fire-21-28-agosto.json"
    );
    const data = await response.json();
    this.firesDataList = data;
  },
};
</script>
<style>
*{
  margin:0;
  padding: 0;
}

html, body {
  max-width: 100%;
  overflow-x: hidden;
}
#app {
  background-color: #E9967A;
  color: #000;
  width: 100vw;
  height: 100vh;
  font-family: 'Playfair Display', serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin: 0px;
}


</style>
