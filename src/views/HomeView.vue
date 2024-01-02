<script setup>
import UserComponent from '@/components/UserComponent.vue'
import FoodComponent from '@/components/FoodComponent.vue'
import RateComponent from '@/components/RateComponent.vue'

function switchContent(articleId) {
    const articles = document.getElementsByClassName('article-params');
    for( var i = 0; i < articles.length; i++) {
        articles.item(i).classList.add('not-visible');  
        if(articles.item(i).id === articleId) {
            articles.item(i).classList.remove('not-visible');
        }
    }
}

</script>

<template>
<div>
    <nav style="width: 100%;">
        <button @click="switchContent('article-user')">User</button>
        <button @click="switchContent('article-food')">Food</button>
        <button @click="switchContent('article-rate')">Rate</button>
    </nav>
</div>
<div>
    <UserComponent />
    <FoodComponent />
    <RateComponent />
</div>

</template>

<style lang="css">

    .article-params {
        text-align: center;
        color: #000000;
        padding-top: 10px;
    }

    nav {
        margin: 0;
        padding: 0;
        background-color: #333;
        height: 49px;
    }

    button {
        float: left;
    }

    button {
        display: block;
        color: #FFFFFF;
        text-align: center;
        padding: 15px 12px;
        padding-left: 30px;
        padding-right: 30px;
        background-color: #333;
        font-size: 16px;
        border: none;
    }

    button:hover {
        background-color: #000000;
    }

    .visible {
        display: block;
    }

    .not-visible {
        display: none;
    }
</style>
