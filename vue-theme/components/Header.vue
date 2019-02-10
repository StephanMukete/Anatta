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
        justify-content: center;
        justify-items: center
    }
</style>
