<template>
    <v-dialog max-width="600px" v-model="dialog">
        <template v-slot:activator="{on}">
            <v-btn class="purple lighten-3" v-on="on">Create new video</v-btn>
        </template>
        <v-card>
            <v-card-title>
                <h2 class="grey--text">Add new video</h2>
            </v-card-title>
            <v-card-text>
                <v-form>
                    <v-text-field label="Title" v-model="title" prepend-icon="mdi-folder"></v-text-field>
                    <v-textarea label="Description" v-model="description" prepend-icon="mdi-pencil"></v-textarea>
                    <v-text-field label="URL" v-model="url" prepend-icon="mdi-microsoft-internet-explorer"></v-text-field>
                    <v-select v-model="category" :items="items" label="Category" required prepend-icon="mdi-account-supervisor-circle"></v-select>
                    <v-text-field label="Subcategory" v-model="subcategory" prepend-icon="mdi-account-box-multiple"></v-text-field>
                    <v-text-field label="Author" v-model="author" prepend-icon="mdi-clipboard-account"></v-text-field>
                    <v-btn text class="purple lighten-3 mx-0 mt-3 ml-8" @click.prevent="submit" :loading="loading">Add video</v-btn>
                </v-form>
            </v-card-text>
        </v-card>
    </v-dialog>
</template>
<script>
import axios from 'axios';
export default {
     data(){
         return{
             items:['Web Development', 'Programming'],
             title:'',
             description:'',
             url:'',
             category:'',
             subcategory:'',
             author:'',
             loading:false,
             dialog:false,
         }
    },
    methods:{
        submit(){
            this.loading = true;
            axios.post('http://127.0.0.1:8000/api/videos/',{
                title: this.title,
                description: this.description,
                url: this.url,
                category: this.category,
                subcategory: this.subcategory,
                author: this.author,
            })
            .then(()=>{
                this.loading=false;
                this.dialog=false;
                this.$emit('videoAdded')
            })
            .catch(res => console.log(res))
        }
    },

}
</script>