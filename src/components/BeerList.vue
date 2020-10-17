<template>
<div>
  <p>BeerList</p>
  <beer-item v-for="(beer, index) in beerList" :key="index" :beerInfo="beer" />
  <button @click="showMore">Showmore</button>
</div>
</template>

<script>
import BeerItem from '../components/BeerItem.vue';
import axios from 'axios';

export default {
  name: 'BeerList',
  components: { BeerItem },
  data: function() {
    return {
      currentPage: 1,
      beerList: []
    }
  },
  created: function() {
    axios.get(`https://api.punkapi.com/v2/beers?page=${this.currentPage}&per_page=5`)
        .then(response => this.beerList = this.beerList.concat(response.data))
        .catch(error => console.log(error))
  },
  methods: {
    showMore() {
      this.currentPage++;
      axios.get(`https://api.punkapi.com/v2/beers?page=${this.currentPage}&per_page=5`)
        .then(response => this.beerList = this.beerList.concat(response.data))
        .catch(error => console.log(error))
    }
  }
}
</script>

<style>

</style>