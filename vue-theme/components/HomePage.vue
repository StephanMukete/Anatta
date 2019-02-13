<template>
  <section class="container">
    <!-- <img id = "banner" :src="preview.homepage_banner[0].image.url" alt="homepage phote"> -->
     <!-- <img :src="preview.image1.url" alt="homepage"> -->
    <img id = "banner" :src="preview.cover_photo.url" alt="homepage">  

  </section>
</template>

<script>
import Prismic from "prismic-javascript"

export default {

  async asyncData(context) {
  var apiEndpoint ="https://vue-theme.cdn.prismic.io/api/v2";
  let preview = {};
 
  const api = await Prismic.getApi(apiEndpoint);
  const result = await api.getByUID( 
    'homepage','homepage'
  );
 // const result = await api.query(Prismic.Predicates.at("document.type", "blog"));
  preview = result.data;
  preview.title = result.data.Title;
  //console.log(result.data.title[0].text)
  console.log(preview);
    // console.log(preview.description[0].text)
  return {preview};
  // .then(function(api) {
  //   return api.query("");
  // })
  // .then (
  //   function(response) {
  //     console.log("Document: ", response.results);
  //   },
  //   function(err) {
  //     console.log("Something went wrong: ", err);
  //   }
  // );
 },
 data(){
   return {
preview
   }
 }

}
</script>

<style scoped>
img{
  width:100%;
  height: 100%;
}
#banner {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
}
</style>
