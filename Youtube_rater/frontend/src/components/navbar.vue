<template>
    <nav>
        <v-snackbar max-height="10px" v-model="snackbar1" :timeout="4000" top>
            <span>successfully Logged In</span>
            <v-btn text color="pink" @click="snackbar1=false" class="ml-8">Close</v-btn>
        </v-snackbar>
        <v-app-bar app color="red" dense dark flat>
            <v-app-bar-nav-icon @click="drawer=!drawer"></v-app-bar-nav-icon>

            <v-toolbar-title>Youtube Rater</v-toolbar-title>

            <v-spacer></v-spacer>
            <v-dialog max-width="400px" v-model="dialog">
                <template v-slot:activator="{on}">
                    <v-btn text v-on="on" v-if="token==null">
                        <v-icon>mdi-lock</v-icon>
                        <span>Login</span>
                    </v-btn>
                </template>
                <v-card flat> 
                    <v-card-title> Log In </v-card-title>
                    <v-form class="pa-6">
                        <v-text-field label="Username" v-model="username" append-icon="mdi-account"></v-text-field>
                        <v-text-field v-model="password" :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"  :type="show1 ? 'text' : 'password'" label="Password" counter @click:append="show1 = !show1"></v-text-field>
                        <v-btn text class="purple lighten-3" @click="submit">Log In</v-btn>
                    </v-form>
                </v-card>
            </v-dialog>

            <v-btn icon>
                <v-icon>mdi-heart</v-icon>
            </v-btn>

            <v-btn icon>
                <v-icon>mdi-magnify</v-icon>
            </v-btn>
            <v-menu offset-y>
                <template v-slot:activator="{on}">
                    <v-btn text v-on="on" v-if="token!=null">
                        <v-icon>mdi-dots-vertical</v-icon>
                    </v-btn>
                </template>
                <v-list>
                    <v-list-item-title class="pa-2 ml-7">Welcome</v-list-item-title>
                    <v-list-item-title class="pa-2">
                        <v-btn @click="logout()">Log out<v-icon right>mdi-exit-to-app</v-icon></v-btn>
                    </v-list-item-title>
                </v-list>
            </v-menu>
        </v-app-bar>

        <v-navigation-drawer v-model="drawer" class="grey darken-4" app>
            <v-row justify="center" class="mt-8">
                <v-avatar size="100">
                    <img src="/john.png/" >
                </v-avatar>
            </v-row>
            <v-row justify="center"> 
                <p class="white--text mt-5">
                    Ashish Maharjan
                </p>
            </v-row>
        </v-navigation-drawer>
    </nav>
</template>

<script>
import axios from 'axios'
export default {
    data(){
        return{
            drawer:false,
            show1:false,
            username:'',
            password:'',
            token:localStorage.getItem('user-token') || null,
            snackbar1:false,
            dialog:false,
        }
    },
    methods:{
        submit(){
            axios.post('http://127.0.0.1:8000/auth/',{
                username: this.username,
                password: this.password,
            })
            .then(resp =>{
                this.token = resp.data.token;
                localStorage.setItem('user-token',resp.data.token);
                this.dialog=false;
                this.snackbar1=true;
                window.location.reload()
            })
            .catch(err => {
                localStorage.removeItem('user-token')
            })
        },
        logout(){
            localStorage.removeItem('user-token');
            this.token = null;
            window.location.reload()
        }
    },
}
</script>