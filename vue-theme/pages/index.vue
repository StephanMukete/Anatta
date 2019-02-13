<template>
  <section class="container">
    <Header/>
    <!-- <img id = "banner" :src="preview.homepage_banner[0].image.url" alt="homepage phote"> -->
     <!-- <img :src="preview.image1.url" alt="homepage"> -->
    <img id = "banner" :src="preview.cover_photo.url" alt="homepage">  

  </section>
</template>

<script>
import Prismic from "prismic-javascript"
import Header from '~/components/Header.vue'



export default {
    components: {
    Header
  },
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

   }
 }

}
</script>

<style>
img{
  width:100%;
  height: 100%;
}
#banner {
  position: absolute;
  top: 0px;
  left: 0px;
  right: 0px;
  width: 100%;
  height: 100%;
  z-index: -1;
}
/* .container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
} */
</style>
