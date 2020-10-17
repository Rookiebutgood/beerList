<template>
<div class="beer-list">
  <p>BeerList</p>
  <beer-item v-for="(beer, index) in beerList" :key="index" :number="index" :beerInfo="beer" @edit="editInfo = $event" />
  <button v-if="showLoadMore" @click="showMore">{{loading ? 'Loading' : 'ShowNext'}}</button>
  <edit-form v-if="editInfo.name" :info="editInfo" @/>
</div>
</template>

<script>
import BeerItem from '../components/BeerItem.vue';
import EditForm from '../components/EditForm.vue';
import axios from 'axios';

export default {
  name: 'BeerList',
  components: { BeerItem, EditForm },
  data: function() {
    return {
      currentPage: 1,
      loading: false,
      showLoadMore: false,
      beerList: [],
      editInfo: {}
    }
  },
  created: function() {
    window.localStorage.setItem('beer', JSON.stringify([]));
    axios.get('https://api.punkapi.com/v2/beers?page=1&per_page=1')
        .then(response => {
          this.beerList = response.data;
        })
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
    },
    edit(e) {
      console.log(e)
    }
  }
}
</script>

<style lang="scss">
  .beer-list {
    width: 100%;
    padding: 0 20%;
    box-sizing: border-box;
  }
</style>