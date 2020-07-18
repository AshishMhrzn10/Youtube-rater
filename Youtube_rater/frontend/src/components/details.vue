<template>
    <div class="text-center">
        <p><b>Title:  </b>{{videodetail.title}}</p>
        <br>
        <p><b>Category:  </b>{{videodetail.category}}</p>
        <br>
        <p><b>Subcategory:  </b>{{videodetail.subcategory}}</p>
        <br>
        <p><b>Description:  </b>{{videodetail.description}}</p>
        <br>
        <iframe width="350" height="225" v-bind:src=videodetail.url></iframe>
        <br>
        <p><b>Rating:  </b>{{videodetail.rating_average}} </p>
        <br>
        <br>
        <b>Comments:</b>
        <br>
        <v-text-field label="Give a rating" type="number" v-bind:value=videodetail.rating_average></v-text-field>
        <v-text-field label="Leave a comment" v-bind:value=videodetail.comments_list></v-text-field>
    </div>
</template>

<script>
export default {
    props:{
        videodetail:{}
    },
}
</script>

<style scoped>
    b{
        color:indigo;
    }
</style>