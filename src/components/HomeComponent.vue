<template>
  <v-container class="fill-height">
    <v-row align="center" justify="center" class="fill-height">
      <v-col cols="6 d-flex flex-row-reverse">
        <div class="grid">
          <img v-for="logo in logos" :key="logo" 
            class="grid-item" alt="d4b6 logo"
            :src="require(`@/assets/${logo.img}`)">
        </div>
      </v-col>
      <v-col cols="6">
        <v-list v-for="job in jobs" :key="job" class="d-flex bg-blue-grey-lighten-5 stagger-list">
          <div class="stagger-item">
            <img class="d-inline" :src="require(`@/assets/check.svg`)"><h2 class="ml-4 d-inline">{{ job.title }}</h2>
          </div>
        </v-list>
        <v-divider class="my-2 divider" thickness=3></v-divider>
        <v-list v-for="(contact, index) in contacts" :key="index" class="bg-blue-grey-lighten-5">
          <div v-if="index === 0">
            <img :src="require(`@/assets/mail.svg`)">
            <a class="ml-4" href="" @click.stop.prevent="snackbar">
              <img alt="d4b6 logo" :src="require(`@/assets/${contact.img}`)">
            </a>
          </div>
          <div v-else>
            <img :src="require(`@/assets/mail.svg`)">
            <a class="ml-4" :href="`${contact.link}`" target="_blank">
              <img alt="d4b6 logo" :src="require(`@/assets/${contact.img}`)">
            </a>
          </div>
        </v-list>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import anime from 'animejs'

export default {
  name: 'HomeComponent',
  data() {
    return {
      logos: [
        {
          img: 'logo-1.png'
        },
        {
          img: 'logo-2.png'
        },
        {
          img: 'logo-3.png'
        },
        {
          img: 'logo-4.png'
        }
      ],
      jobs: [
        {
          title: 'Web Development'
        },
        {
          title: 'Web Design'
        },
        {
          title: 'Graphic Design'
        }
      ],
      contacts: [
        {
          alt: 'd4b6 Yahoo Link',
          link: 'mailto:damir.bubanovic@yahoo.com',
          img: 'yahoo-logo.svg'
        },
        {
          alt: 'd4b6 Github Link',
          link: 'https://github.com/damir-bubanovic',
          img: 'github-logo.svg'
        },
        {
          alt: 'd4b6 Stack Overflow Link',
          link: 'https://stackoverflow.com/users/11778242/damir-bubanovic',
          img: 'so-logo.svg'
        },
      ],
      // stagger: 'stagger-right-enter-active'
    }
  },
  mounted() {
    anime({
      targets: '.grid .grid-item',
      loop: true,
      direction: 'alternate',
      translateX: anime.stagger(10, {grid: [14, 5], from: 'center', axis: 'x'}),
      translateY: anime.stagger(10, {grid: [14, 5], from: 'center', axis: 'y'}),
      rotateZ: anime.stagger([0, 90], {grid: [14, 5], from: 'center', axis: 'x'}),
      delay: anime.stagger(600, {grid: [14, 5], from: 'center'}),
      easing: 'spring(1, 80, 10, 0)'
    });
    anime({
      targets: '.stagger-list .stagger-item',
      translateX: -200,
      direction: 'reverse',
      delay: anime.stagger(200, {from: 'center'}),
    });
  },
  methods: {
    snackbar() {
      this.$emit('snackbarEmail', true);
    }
  }
}
</script>

<style>
  .grid {
    width: 210px;
    height: 210px;
  }
  .grid-item {
    width: 100px;
    height: 100px;
    display: inline-block;
    float: left;
  }
  .divider {
    color: #004D40;
  }
</style>