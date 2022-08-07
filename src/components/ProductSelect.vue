<template>
  <div class="products__select">
    <select class="select"  @change="$emit('sort-items', $event.target.value)">
      <option selected disabled>По умолчанию</option>
      <option value="name">По названию</option>
      <option value="max">По цене max</option>
      <option value="min">По цене min</option>
    </select>
  </div>
</template>

<script>
export default {
  emits: ['sort-items']
}
</script>

<style>

</style>