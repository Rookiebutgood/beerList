<template>
<div class="beer-list">
  <beer-item v-for="(beer, index) in beerList" :key="index" 
             :number="index" 
             :beerInfo="beer" 
             @edit="editItem" 
             @delete="deleteItem" />
  <button class="beer-list__btn" v-if="showLoadMore" @click="showMore">{{isLoading ? 'Loading' : 'ShowNext'}}</button>
  <edit-form v-if="showEditForm" :info="editInfo" @save="saveItem" />
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
      isLoading: false,
      showLoadMore: false,
      showEditForm: false,
      beerList: [],
      editInfo: {},
    }
  },
  created: function() {
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
      this.isLoading = true;
      axios.get(`https://api.punkapi.com/v2/beers?page=${this.currentPage}&per_page=25`)
        .then(response => {
          if(response.data.length > 0) {
            this.beerList = this.beerList.concat(response.data)
          } else {
            this.showLoadMore = false
          }
        })
        .catch(error => console.log(error))
        .finally(() => this.isLoading = false)
    },
    editItem(info) {
      this.showEditForm = true;
      this.editInfo = info;
    },
    saveItem(info) {
      if(info.id) {
          this.beerList.map(el => {
          if(info.id === el.id) {
            el.name = info.name;
            el.description = info.description;
          }
        });
      }
      this.showEditForm = false;
    },
    deleteItem(id) {
      this.beerList = this.beerList.filter(el => {return el.id != id});
    }
  }
}
</script>

<style lang="scss">
  .beer-list {
    width: 100%;
    padding: 0 20%;
    box-sizing: border-box;
    position: relative;
    &__btn {
      border: 1px solid black;
      background: none;
      outline: none;
      border-radius: 5px;
      padding: 5px;
      cursor: pointer;
      margin: 0 10px;
      &:hover {
        border: none;
        box-shadow: 1px 1px 10px 1px rgba(0, 0, 0, 0.5);
      }
    }
  }
</style>