<template>
  <div>
    <input type="text" v-model="name">
    <textarea v-model="description"></textarea>
    <button @click="$emit('save', {id, name, description})">Сохранить</button>
    <button @click="$emit('save', {})">Удалить</button>
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

<style>

</style>