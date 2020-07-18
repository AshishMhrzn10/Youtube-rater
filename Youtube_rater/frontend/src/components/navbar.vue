<template>
    <nav>
        <v-app-bar app color="red" dense dark flat>
            <v-app-bar-nav-icon @click="drawer=!drawer"></v-app-bar-nav-icon>

            <v-toolbar-title>Youtube Rater</v-toolbar-title>

            <v-spacer></v-spacer>

            <v-btn icon>
                <v-icon>mdi-heart</v-icon>
            </v-btn>

            <v-btn icon>
                <v-icon>mdi-magnify</v-icon>
            </v-btn>
            <v-menu offset-y>
                <template v-slot:activator="{on}">
                    <v-btn text v-on="on">
                        <v-icon>mdi-dots-vertical</v-icon>
                    </v-btn>
                </template>
                <v-list>
                    <v-list-item-title class="pa-2">Welcome, Ashish</v-list-item-title>
                    <v-list-item-title class="pa-2">Log out
                        <v-icon right>mdi-exit-to-app</v-icon>
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
export default {
    data(){
        return{
            drawer:false,
        }
    }
}
</script>