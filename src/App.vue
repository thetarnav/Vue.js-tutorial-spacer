<template>
  <div class="app">
    <HeroImage />
    <Claim />
    <Input v-model="searchValue" @input="handleInput"/>
    <div class="images">
      <!-- <div class="images--item" v-for="item in results" :key="item.nasa_id">
        <img :src="item.img">
      </div> -->
    </div>
  </div>
</template>

<script>
// Vue Components:
import Claim from "@/components/Claim";
import Input from "@/components/Input";
import HeroImage from "@/components/HeroImage";

// JavaScript libraries:
const axios = require('axios');
const debounce = require('lodash.debounce');

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'App',
  components: {
    Claim,
    Input,
    HeroImage
  },
  data() {return {
    searchValue: '',
    results: [],
  }},
  methods: {
    // eslint-disable-next-line
    handleInput: debounce(function() {
      if (this.searchValue == '') return
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          let items = response.data.collection.items;
          if (items.length == 0) return
          this.results = items.map(item => {
            return {
              nasa_id: item.data[0].nasa_id,
              title: item.data[0].title,
              date: item.data[0].date_created,
              img: item.links[0].href
            }
          });
        }).catch((err) => {
          console.error(error);
        });
    }, 600),
  },
};
</script>

<style lang="scss">
@import '@/scss/font-faces';

* {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
*, *::after, *::before {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
html {
  @include text;
}
</style>

<style lang="scss" scoped>
.app {
  width: 100%;
  min-height: 100vh;
  padding-top: 30vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
