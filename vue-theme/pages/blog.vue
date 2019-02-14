<template>
  <section class="container">
    <Header/>
      <h1>{{preview.title[0].text}}</h1>
                     <div class="onbanner">
                <img :src="preview.image1.url" alt="blog cover photo"> 
                <h5>{{preview.Image1_title[0].text}}</h5>
                <h3>{{preview.Image1_subtitle[0].text}}</h3>
                <p>{{preview.description[0].text}}</p>
         </div>
      <div id="banner">
      
              <img  :src="preview.cover_image.url" alt="homepage">
      <div class="space">
        <font-awesome-icon :icon="['fab', 'facebook']" />
        <font-awesome-icon :icon="['fab', 'twitter']" />
        <font-awesome-icon :icon="['fab', 'instagram']" />
        <font-awesome-icon :icon="['fab', 'youtube']" />
      </div>
        
        <div id="banner2" v-for="i in Math.ceil(photos.length / 2)" :key=i.id>
        
        <h2>be updated</h2>
        <p>subscribe to my channel to make sure you dont miss any info</p>
            <div class="content">
      <form name="contact" action="" method="post">
        <label class="form-label" for="email">
          Email:
        </label>
        <input class="form-field" name="email" id="email" />

        <input class="form-button" type="submit" value="Subscribe" />
      </form>
    </div>
        
              <span class="rowq" v-for=" photo in photos.slice((i-1)*2, i*2)" :key=photo.id>
          <!-- <div  id="banner2" v-for="photo in photos" :key=photo.id> -->
                <img :src="photo.gallery_image.url" alt="image1"> 
              
              </span>
             
           </div>
           
                        <div class="col3" v-for="i in Math.ceil(blogs.length / 2)" :key=i.id>
              <span class="rowq" v-for=" blog in blogs.slice((i-1)*2, i*2)" :key=blog.id>

            <img :src="blog.image_banner.url" alt="image1">
            <h5> {{blog.title_of_banner[0].text}} </h5>
            <h2> {{blog.subtitle_of_banner[0].text}} </h2>
            <p> {{blog.description[0].text}} </p>
              </span>
          </div>
          
    <Footer/>
        
      </div>
  

  </section>
</template>

<script>
import Prismic from "prismic-javascript"
import Header from '~/components/Header.vue'
import Footer from '~/components/Footer.vue'

// import Header from '~/components/Header.vue'

export default {
    components: {
    Header,
    Footer
  },
  async asyncData(context) {
  var apiEndpoint ="https://vue-theme.cdn.prismic.io/api/v2";
  let preview = {};
  let photos = [];
  let blogs = [];
 
  const api = await Prismic.getApi(apiEndpoint);
  const result = await api.getByUID( 
    'blogs','blogs'
  );
 // const result = await api.query(Prismic.Predicates.at("document.type", "blog"));
  preview = result.data;
  photos = preview.body[1].items;
  blogs = preview.body[0].items;
  console.log(blogs);
  return {
      preview,
      photos,
      blogs
    };
 },
 data(){
   return {

   }
 }

}
</script>

<style scoped>

img{
  width:100%;
  height: 100%;
}


.onbanner{
    margin-top: 15%;
    height: 27rem;
    width:18rem;
    margin-left: 60%;
    background: white;
    position: absolute;
}
 .onbanner img{
    height: 50%;
    width:100%;
    /* margin-top: 20rem; */
    /* margin-left: 20rem */
}
.flex{
    display: flex;
    float: left;
    flex-direction: column;

     /* flex-wrap: nowrap; */
}
/* .flex .col11{
  width: 30%;
  height: 100%;} */
.f{
      display: flex;
      flex-direction: column;
      
  /* grid-template-columns: repeat(2, 1fr); */
/* margin-top: 10rem;
margin-left: 40rem;  */
/* height: 10rem; */
}
.flex2{
      display: flex;
      flex-direction: column;
      
  /* grid-template-columns: repeat(2, 1fr); */
margin-top: 10rem;
margin-left: 20rem; 
/* height: 10rem; */
}
.col3 img {
    width: 50%;
    height: 50%;
}
.flex2 h2 {
    width: 50%;
    height: 50%;
}
.flex2 p {
    width: 50%;
    height: 50%;
}
.col22 img {
  top:0;
    width: 90%;
    height: 50%;
}
.space{
    height: 10rem;
}

.col3{
  position: relative;
  top: 30;
margin-left: 20rem; 
    display: grid;
  grid-template-columns: repeat(2, 1fr);
}

</style>
