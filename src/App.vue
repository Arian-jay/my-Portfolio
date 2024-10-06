<template>
  <v-app>
    <v-main>
      <MyPortfolio/>
    </v-main>
  </v-app>
</template>

<script>
import MyPortfolio from './components/MyPortfolio.vue';

export default {
  name: 'App',

  components: {
    MyPortfolio,
  },

  data: () => ({
    //
  }),
}
</script>
