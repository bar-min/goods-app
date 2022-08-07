<template>
  <div class="modal" :class="{ 'modal-active': show }">
    <p class="modal__message">Успешное добавление товара</p>
  </div>
</template>

<script>
export default {
  props: ['show']
}
</script>

<style>

</style>