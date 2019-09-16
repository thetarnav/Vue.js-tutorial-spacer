<template>
  <div class="wrapper">
    <input
      type="text"
      class="search"
      id="search-input"
      placeholder="Search some space stuff"
      v-model="searchValue"
      @input="handleInput"
    />
    <div class="images">
      <div class="images--item" v-for="item in results" :key="item.nasa_id">
        <img :src="item.img">
      </div>
    </div>
  </div>
</template>

<script>
const axios = require('axios');
const debounce = require('lodash.debounce');

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',
  data() {
    return {
      searchValue: '',
      results: [],
    }
  },
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

<style lang="scss" scoped>
.wrapper {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #333;
}
.search {
  padding: 0 5px;
  margin-top: 50%;
  height: 35px;
  width: 250px;
  border: none;
  background: white;
}
</style>
