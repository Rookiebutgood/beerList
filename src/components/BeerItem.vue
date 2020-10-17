<template>
  <div class="beer-item">
    <span class="beer-item__number">{{number+1}}</span>
    <img :src="beerInfo.image_url" class="beer-item__img" />
    <div>
      <h2 class="beer-item__title">{{beerInfo.name}}</h2>
      <p class="beer-item__description">{{beerInfo.description}}</p>
      <blockquote class="beer-item__tips">{{beerInfo.brewers_tips}}</blockquote>
      <button @click="edit(beerInfo)">Edit</button>
      <button @click="$emit('delete', beerInfo.id)">Delete</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BeerItem',
  props: ['beerInfo', 'number'],
  methods: {
    edit: function(info) {
      this.$emit('edit', info)
    }
  }
}
</script>

<style lang="scss">
  .beer-item {
    display: flex;
    border-radius: 10px;
    box-shadow: 1px 1px 10px 1px rgba(0, 0, 0, 0.7);
    padding: 10px;
    margin-bottom: 20px;
    &__img {
      width: 10%;
      height: auto;
    }
    &__tips {
      border-left: 5px solid black;
      padding-left: 10px;
      text-align: left;
    }
  }
</style>