<template>
  <div class="footer">

   <div id="mentions">
     <p>{{ mention }}</p>
   </div>
  </div>
</template>
<script>
export default {
  name: "FooterMap",
  data(){
   return{
     mention : '2021 | by Francesca Grimaldi'
   }
 }
};
</script>
<style>
.footer{
  display: contents;
  margin: 0 auto;
  position: fixed;
  width: 100%;
  z-index: 999;
  text-align: center;
}

#mentions p {
  font-size:1em;
}

</style>
