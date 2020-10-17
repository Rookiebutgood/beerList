<template>
  <div class="beer-item">
    <span class="beer-item__number">{{number+1}}</span>
    <img :src="beerInfo.image_url" class="beer-item__img" />
    <div class="beer-item__info">
      <h2 class="beer-item__title">{{beerInfo.name}}</h2>
      <p class="beer-item__description">{{beerInfo.description}}</p>
      <blockquote class="beer-item__tips">{{beerInfo.brewers_tips}}</blockquote>
      <div class="beer-item__buttons">
        <button class="beer-item__btn" @click="$emit('edit', beerInfo)">Edit</button>
        <button class="beer-item__btn" @click="$emit('delete', beerInfo.id)">Delete</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BeerItem',
  props: ['beerInfo', 'number']
}
</script>

<style lang="scss">
  .beer-item {
    display: flex;
    align-items: center;
    border-radius: 10px;
    box-shadow: 1px 1px 10px 1px rgba(0, 0, 0, 0.5);
    padding: 10px;
    margin-bottom: 20px;
    &__number {
      font-size: 20px;
      font-weight: bold;
      width: 5%;
      align-self: flex-start;
    }
    &__img {
      width: 10%;
      height: auto;
    }
    &__info {
      width: 85%;
      padding-left: 30px;
    }
    &__description {
      text-align: left;
    }
    &__tips {
      border-left: 5px solid black;
      padding-left: 10px;
      text-align: left;
    }
    &__buttons {
      text-align: right;
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