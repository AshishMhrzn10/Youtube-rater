<template>
  <v-app style="background:#F5F5F5;">
    <Navbar/>
    <Main/>
    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
import Navbar from '@/components/navbar'
import Main from '@/components/main'
export default {
  name: 'App',

  components: {Navbar,Main},

  data: () => ({
    //
  }),
};
</script>
