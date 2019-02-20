<template>
  <section class="container">
    <Header/>
        <h1>{{preview.title[0].text}}</h1>
            <div class="onbanner">
              <img :src="preview.image1.url" alt="blog cover photo"> 
              <h5>{{preview.Image1_title[0].text}}</h5>
              <h3>{{preview.Image1_subtitle[0].text}}</h3>
              <p>{{preview.description[0].text}}</p>
              <nuxt-link to="#">Read More</nuxt-link>
            </div>
            <div id="banner">
                <div class="cover-photo">
                    <img  :src="preview.cover_image.url" alt="blog photo">
                </div>
            <div class="space">
                <Icon/>
            </div>

            <div id="banner2" v-for="i in Math.ceil(photos.length / 2)" :key=i.id>
                <div class="content">
                    <form  name="contact" action="" method="post">
                        <div class="box">
                            <h2>be updated</h2>
                            <p>subscribe to my channel to make sure you dont miss any info</p>
                            <label class="form-label" for="email">
                                Email:
                            </label>
                            <input class="form-field" name="email" id="email" />
                            <input class="form-button" type="submit" value="Subscribe" />
                        </div>
                        <span class="row" v-for=" photo in photos.slice((i-1)*2, i*2)" :key=photo.id>    
                            <img :src="photo.gallery_image.url" alt="image1">   
                        </span>
                    </form>
                </div>
            </div>
        <div class="blogs">
            <div class="col3" v-for="i in Math.ceil(blogs.length / 2)" :key=i.id>
                <span class="rowq" v-for=" blog in blogs.slice((i-1)*2, i*2)" :key=blog.id>
                    <img :src="blog.image_banner.url" alt="image1">
                    <h5> {{blog.title_of_banner[0].text}} </h5>
                    <h2> {{blog.subtitle_of_banner[0].text}} </h2>
                    <p> {{blog.description[0].text}} </p>
                </span>
            </div>
        </div>

            <Footer/>
        </div>
    </section>
</template>

<script>
import Prismic from "prismic-javascript"
import Header from '~/components/Header.vue'
import Footer from '~/components/Footer.vue'
import Icon from '~/components/Icon.vue'

export default {
    components: {
    Header,
    Footer,
    Icon,
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

      preview = result.data;
      photos = preview.body[1].items;
      blogs = preview.body[0].items;
      console.log(blogs);
      return {
          preview,
          photos,
          blogs
      };
    }
}
</script>

<style scoped>
.col3{
    margin-left:20rem;
 }

.col3 img {
    width: 100%;
    height: 16rem;
}
  

/* Section for media queries */

@media screen and (min-width: 1171px) {

    .col3{
        margin-left:25rem;
        margin-top: 0;
    }
}

@media screen and (min-width: 769px) and (max-width: 170px) {

}

@media screen and (max-width: 768px) {

    .col3{
    margin-left:0;
    }

    .col3 img {
        width: 100%;
        height: 20rem;
    }

    .blogs{
        margin-top:85rem;
    }

    .col3{
    
        display: grid;
        grid-template-columns: repeat(2, 1fr);
    }
}
@media screen and (max-width: 500px) {
  
    .blogs{
        margin-top:70rem;
    }
  
  .col3{

        grid-template-columns:  1fr;
    }
}

</style>
