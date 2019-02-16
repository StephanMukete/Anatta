<template>
    <footer class="footer">
        <ul class="nav-items">
            <li>
                <nuxt-link to="/">Home</nuxt-link>
            </li>
            <li>
                <nuxt-link to="/blog">Blog</nuxt-link>
            </li>
            <li><font-awesome-icon :icon="['fab', 'facebook']" /> </li>
            <li><font-awesome-icon :icon="['fab', 'twitter']" /></li>
            <li><font-awesome-icon :icon="['fab', 'instagram']" /></li>
            <li> <font-awesome-icon :icon="['fab', 'youtube']" /></li>
        </ul>
         <div class="copyright">
             ©2019 Dr Chattergee All rights reserved 
        </div>
    </footer>   
</template>
      