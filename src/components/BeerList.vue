<template>
<div class="beer-list">
  <beer-item v-for="(beer, index) in beerList" :key="index" 
             :number="index" 
             :beerInfo="beer" 
             @edit="editItem" 
             @delete="deleteItem" />
  <div>
    <button class="beer-list__btn" v-if="showLoadMore" @click="showMore">{{isLoading ? 'Loading' : 'Show next'}}</button>
    <label>Количество записей</label>
    <select class="beer-list__select" v-model="perPage">
      <option value="1">1</option>
      <option value="5">5</option>
      <option value="10">10</option>
      <option value="25">25</option>
      <option value="50">50</option>
    </select>
  </div>
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
      perPage: 10
    }
  },
  created: function() {
    axios.get('https://api.punkapi.com/v2/beers?page=1&per_page=10')
        .then(response => {
          this.beerList = response.data;
        })
        .catch(error => console.log(error))
        .finally(() => this.showLoadMore = true)
  },
  methods: {
    //Метод для получения новых записей из api. Если api возвращает пустой массив, скрывает кнопку Show next
    showMore() {
      this.currentPage++;
      this.isLoading = true;
      axios.get(`https://api.punkapi.com/v2/beers?page=${this.currentPage}&per_page=${this.perPage}`)
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
    //Метод для передачи данных из BeerItem в EditForm
    editItem(info) {
      this.showEditForm = true;
      this.editInfo = info;
    },
    //Метод для сохранения изменений, сделанных в EditForm
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
    //Метод для удаления записи
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
    &__select {
      margin-left: 10px;
    }
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