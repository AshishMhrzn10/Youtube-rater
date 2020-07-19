<template>
<div>
    <div class="text-center grey lighten-3">
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
    </div>
    <div class="grey lighten-1">
        <v-form class="pa-2" @submit="$emit('updated',videodetail)"> 
        <b>Comments:</b>
        <br>
        <v-text-field label="Give a rating" type="number" v-model="stars" v-bind:value=stars hint="On the total of 5"></v-text-field>
        <v-text-field label="Leave a comment" v-model="comments" v-bind:value=videodetail.comments_list></v-text-field>
            <v-btn class="warning" @click="update" type="submit">Update</v-btn>
        </v-form>
        
    </div>
    <br>
    <v-form @submit="$emit('deleted',videodetail)">
    <v-btn color="red lighten-1" @click="videoDelete(videodetail)" type="submit">Delete video</v-btn>
    </v-form>
</div>
</template>

<script>
import {TokenService} from '../storage/service'
import axios from 'axios'
export default {
    data(){
        return{
            comments:'',
            stars:'',
        }
    },
    props:{
        videodetail:{}
    },
    methods:{
        videoDelete(videodetail){
            var postData ={
            video: this.videodetail.id,
            };
            let axiosConfig ={
                headers:{
                    'Authorization' : 'Token' + this.token
                }
            };
            axios.delete(`http://127.0.0.1:8000/api/videos/${this.videodetail.id}/`,axiosConfig)
            .then(res =>{
            })
            .catch(err => console.log(err))
        },

        update(stars,comments){
            this.token = TokenService.getToken()
      
            var postData = {
                stars: this.stars,
                comments: this.comments,
                
            };
            let axiosConfig={
                headers:{
                    'Authorization' : 'Token' + this.token
                }
            };
            axios.post(`http://127.0.0.1:8000/api/videos/${this.videodetail.id}/rate_video/`,postData,axiosConfig)
            .then(res =>{
                
            })
            .catch(err => console.log(err))
        },
        
    },
    
    created(){
        let token;
        this.token = TokenService.getToken();
        console.log(this.stars)
    }
}
</script>

<style scoped>
    b{
        color:indigo;
    }
</style>