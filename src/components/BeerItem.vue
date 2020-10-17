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
    border-radius: 10px;
    box-shadow: 1px 1px 10px 1px rgba(0, 0, 0, 0.7);
    padding: 10px;
    margin-bottom: 20px;
    &__img {
      width: 10%;
      height: auto;
    }
  }
</style>