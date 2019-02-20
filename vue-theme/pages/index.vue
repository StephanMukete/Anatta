<template>
    <section class="container">
        <Header/>
            <h1> {{preview.cover_text[0].text}} </h1>
            <div id = "banner">
                <div class="homepage">
<img  :src="preview.cover_photo.url" alt="homepage">
                </div> 
                <div class="col2">
                    <img :src="preview.image1.url" alt="image1"> 
                    <div class="row2">
                        <h4> {{preview.image1_maintext[0].text}} </h4>
                        <p> {{preview.image1_subtext[0].text}} </p>
                    </div>
                </div>
                <div class="col1">
                    <h2> {{preview.highlight_text[0].text}} </h2> 
                    <Logo/>
                    <div id="outerWrap">
                        <div id="layer1">
                            <img :src="preview.book_image.url" alt="image1">
                        </div>
                        <div id="layer2">
                            <h3> {{preview.book_title[0].text}} </h3> 
                            <p> {{preview.book_description[0].text}} </p>
                        </div>
                    </div>
                    <div id="quote">
                        <div class="quote" v-for="quote in quotes" :key=quote.id>
                            <p>{{ quote.quote[0].text }}</p>
                            <div class="col2">
                                <img :src="quote.portrait_author.url" alt="image1">
                                <p>{{ quote.name_of_the_author[0].text }}</p>
                            </div>
                        </div>
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
      </section>
</template>

<script>
import Prismic from "prismic-javascript"
import Header from '~/components/Header.vue'
import Footer from '~/components/Footer.vue'
import Logo from '~/components/Logo.vue'



export default {
    components: {
    Header,
    Footer,
    Logo
  },
    async asyncData(context) {
        let apiEndpoint ="https://vue-theme.cdn.prismic.io/api/v2";
        let preview;
        let quotes = [];
        let blogs = [];
    
        const api = await Prismic.getApi(apiEndpoint);
        const result = await api.getByUID( 
            'homepage','homepage'
        );
    
        preview = result.data;
        preview.title = result.data.Title;
        quotes = preview.body[0].items;
        blogs = preview.body[1].items;
    
        return{
            preview,
            quotes,
            blogs
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
    margin-top: 2rem;
}

.col3 img{
    height: 22rem;
}

/* Media queries section*/
@media screen and (min-width: 1171px) {

  }

@media screen and (min-width: 769px) and (max-width: 170px) {

}

@media screen and (max-width: 768px) {

    .col3{
        grid-template-columns: repeat(2, 1fr);
    }

    .col2 .row2{
        width: 100%;
        height: 80%;
    }
}
@media screen and (max-width: 500px) {
    .col3{
    grid-template-columns: 1fr;
    }
    
    .col2 .row2{
        width: 100%;
        height: 80%;
    }   
}

</style>
