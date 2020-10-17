<template>
  <div>
    <input type="text" :value="info.name">
    <textarea :value="info.description"></textarea>
    <button>Сохранить</button>
    <button>Удалить</button>
  </div>
</template>

<script>
export default {
  name: 'EditForm',
  props: ['info']
}
</script>

<style>

</style>