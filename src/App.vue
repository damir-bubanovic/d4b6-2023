<template>
  <v-app class="bg-blue-grey-lighten-5">
    <v-main>
      <HomeComponent @snackbarEmail="onSnackbarEmail"/>
    </v-main>
    <v-footer app bottom fixed padless class="bg-blue-grey-lighten-5">
      <FooterComponent @snackbarEmail="onSnackbarEmail"/>
    </v-footer>
    <v-snackbar v-model="snackbar.show" :timeout="5000">
      <h2 class="text-center font-weight-bold">{{ snackbar.email }}</h2>
    </v-snackbar>
  </v-app>
</template>

<script>
import HomeComponent from './components/HomeComponent.vue'
import FooterComponent from './components/FooterComponent.vue'

export default {
  name: 'App',
  data() {
    return {
      snackbar: {
        show: false,
        email: 'damir.bubanovic@yahoo.com'
      }
    }
  },
  mounted() {
    document.title = 'd4b6 | Home Page'
  },
  methods: {
    onSnackbarEmail(data) {
      this.snackbar.show = data;
    }
  },
  components: {
    HomeComponent,
    FooterComponent
  },
}
</script>
