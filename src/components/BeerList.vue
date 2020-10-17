<template>
<div>
  <p>BeerList</p>
  <beer-item v-for="(beer, index) in beerList" :key="index" :beerInfo="beer" />
  <button v-if="showLoadMore" @click="showMore">{{loading ? 'Loading' : 'ShowNext'}}</button>
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
      loading: false,
      showLoadMore: false,
      beerList: []
    }
  },
  created: function() {
    axios.get(`https://api.punkapi.com/v2/beers?page=${this.currentPage}&per_page=25`)
        .then(response => this.beerList = this.beerList.concat(response.data))
        .catch(error => console.log(error))
        .finally(() => this.showLoadMore = true)
  },
  methods: {
    showMore() {
      this.currentPage++;
      this.loading = true;
      axios.get(`https://api.punkapi.com/v2/beers?page=${this.currentPage}&per_page=25`)
        .then(response => {
          if(response.data.length > 0) {
            this.beerList = this.beerList.concat(response.data)
          } else {
            this.showLoadMore = false
          }
        })
        .catch(error => console.log(error))
        .finally(() => this.loading = false)
    }
  }
}
</script>

<style>

</style>