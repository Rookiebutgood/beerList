<template>
  <div class="edit-form">
    <input type="text" v-model="name" class="edit-form__name" />
    <textarea v-model="description" class="edit-form__description" />
    <div class="edit-form__buttons">
      <button class="edit-form__btn" @click="$emit('save', {id, name, description})">Save</button>
      <button class="edit-form__btn" @click="$emit('save', {})">Close</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'EditForm',
  props: ['info'],
  data: function() {
    return {
      id: this.info.id,
      name: this.info.name,
      description: this.info.description
    }
  },
}
</script>

<style lang="scss">
  .edit-form {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 400px;
    height: 300px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    background: #fff;
    border-radius: 10px;
    box-shadow: 1px 1px 10px 1px rgba(0, 0, 0, 0.5);
    padding: 10px;
    &__name,
    &__description {
      border: none;
      border-bottom: 1px solid rgba(0, 0, 0, 0.3);
      outline: none;
      margin: 10px;
      padding: 5px;
      font-family: inherit;
      font-size: 18px;
      font-weight: normal;
      &:focus {
        border-bottom: 1px solid black;
      }
    }
    &__description {
      resize: none;
      height: 100%;
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