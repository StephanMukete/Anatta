<template>
  <section class="container">
    <Header/>
     <h1> {{preview.cover_text[0].text}} </h1>
     
    <div id = "banner">
           <img  :src="preview.cover_photo.url" alt="homepage"> 
          <div class="col2">
               <img :src="preview.image1.url" alt="image1"> 
               <div class="row2">
                 <h4> {{preview.image1_maintext[0].text}} </h4>
                 <p> {{preview.image1_subtext[0].text}} </p>
               </div>
              
          </div>
          <div class="col1">
         
             <h2> {{preview.highlight_text[0].text}} </h2> 
                <div class="icons">
              <img src="~/assets/icons/BBC_News.svg" alt="Kiwi standing on oval">
            </div>
            <div id="outerWrap">
              <div id="layer1">
                <img :src="preview.book_image.url" alt="image1">
              </div>
              <div id="layer2">
                              <h3> {{preview.book_title[0].text}} </h3> 
              <p> {{preview.book_description[0].text}} </p>
              </div>
            </div>
<!--             
              <div class="onbanner3">

          </div> -->
              <div class="quote" v-for="quote in quotes" :key=quote.id>
                 <p>{{ quote.quote[0].text }}</p>
                 <img :src="quote.portrait_author.url" alt="image1">
                 <p>{{ quote.name_of_the_author[0].text }}</p>
              </div>
          </div>
          <div class="col2">
           <img :src="preview.blog1_image.url" alt="image1"> 
            <div class="row2">
                <h4> {{preview.blog_highlight[0].text}} </h4>
                <h2> {{preview.blog1_tittle[0].text}} </h2>
                <p> {{preview.blog1_description[0].text}} </p> 
            </div>
          </div>
           <div class="col3" v-for="i in Math.ceil(blogs.length / 3)" :key=i.id>
              <span class="rowq" v-for=" blog in blogs.slice((i-1)*3, i*3)" :key=blog.id>
            <img :src="blog.image_banner.url" alt="image1">
            <h2> {{blog.title_of_banner[0].text}} </h2>
            <p> {{blog.description[0].text}} </p>
          </span>
          </div>
          <Footer />
     
    </div>
    <div class="col2">
        <!-- <img :src="preview.image1.url" alt="image1">  -->
    </div>
  </section>
</template>

<script>
import Prismic from "prismic-javascript"
import Header from '~/components/Header.vue'
import Footer from '~/components/Footer.vue'



export default {
    components: {
    Header,
    Footer
  },
  async asyncData(context) {
  var apiEndpoint ="https://vue-theme.cdn.prismic.io/api/v2";
  let preview;
  let quotes = [];
  let blogs = [];
 
  const api = await Prismic.getApi(apiEndpoint);
  const result = await api.getByUID( 
    'homepage','homepage'
  );
 // const result = await api.query(Prismic.Predicates.at("document.type", "blog"));
  preview = result.data;
  preview.title = result.data.Title;
  quotes = preview.body[0].items;
  blogs = preview.body[1].items;
  //console.log(result.data.title[0].text)
  console.log(blogs);
  //  console.log(quotes);
    // console.log(preview.description[0].text)
  return{
    preview,
    quotes,
    blogs
  }
  
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

<style scoped>

.col2 .row2{
  width: 50%;
  height: 80%;
}

.quote img{
  height: 50px;
  width:50px;
}
.col3{
    display: grid;
  grid-template-columns: repeat(3, 1fr);
}
.col3 img{
      height: 200px;
}
 /* .container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
} */
/*
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
