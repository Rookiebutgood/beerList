<template>
  <div class="beer-item">
    <span></span>
    <img :src="beerInfo.image_url" class="beer-item__img" />
    <div>
      <h2>{{beerInfo.name}}</h2>
      <p>{{beerInfo.description}}</p>
      <blockquote>{{beerInfo.brewers_tips}}</blockquote>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BeerItem',
  props: ['beerInfo']
}
</script>

<style lang="scss">
  .beer-item {
    display: flex;
    &__img {
      width: 10%;
      height: auto;
    }
  }
</style>