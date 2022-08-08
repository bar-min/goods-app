<template>
  <transition name="loader" v-if="loading">
     <div class="loader">
      <div class="loader__item"></div>
    </div>
  </transition>
</template>

<script>
export default {
  props: ['loading']
}
</script>

<style>

</style>