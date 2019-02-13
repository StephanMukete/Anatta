<template>
    <header class="header">
        <ul class="nav-items">
            <li>
                <nuxt-link to="/">Home</nuxt-link>
            </li>
            <li>
                <nuxt-link to="/blog">Blog</nuxt-link>
            </li>
        </ul>
    </header>
</template>

<style scoped>
    .header{
        width: 100%;
        height:60px;
        display: flex;
        justify-content: right;
        float: right;
        justify-items: center;
    }

    .nav-items{
        list-style-type: none;
        padding: 0%;
        margin: 40px;
        display: flex;
        justify-content: space-around;
        float: right;
        width: 20%;
    }
</style>
