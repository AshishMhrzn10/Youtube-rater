<template>
    <div class="mt-10">
         <v-snackbar max-height="10px" v-model="snackbar" :timeout="4000" top>
            <span>Video successfully added</span>
            <v-btn text color="pink" @click="snackbar=false" class="ml-8">Close</v-btn>
        </v-snackbar>
        <v-container>
            <v-row>
                <v-col md='1'>
                </v-col>
            <v-col md='5'>
                <h2 class="mb-6 mt-5 ml-15">Welcome to Youtube Rater</h2>
                <hr>
                <div class="text-center mt-5">
                    <Create @videoAdded='snackbar=true'/>
                </div>
                <v-card class="mx-auto mt-5" max-width="300" v-for="video in videos" :key="video.id">
                    <v-card-text>
                        <h2>{{video.title}}</h2>
                        <p class="mt-3">Rating: {{video.rating_average}}</p>
                    </v-card-text>
                    <v-card-actions>
                    <v-btn text color="deep-purple accent-4" @click="videoDetail(video)">Details</v-btn>
                    </v-card-actions>
                </v-card>
            </v-col>
            <v-col md='6' color="#F5F5F5">
                <div></div>
                <Details :videodetail="videodetail"/>
            </v-col>
            </v-row>
        </v-container>
        
    </div>
</template>
<script>
import axios from 'axios';
import Details from './details';
import Create from './createvideo';
export default {
    data(){
        return{
            videos: [],
            videodetail: Object, 
            snackbar:false,
        }
    },
    components:{Details,Create},
    methods:{
        getVideos(){
            axios.get('http://127.0.0.1:8000/api/videos/')
            .then(res => (this.videos = res.data))
            .catch(err => console.log(err));
        },
        videoDetail(video){
            this.videodetail = video;
            console.log(this.videodetail)
        }
    },
    created(){
        this.getVideos()
    }
}
</script>