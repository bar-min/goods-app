<template>
  <div class="products">
    <div class="products__container">
      <transition-group name="list">
        <div class="products__card card" v-for="product in products" :key="product.id">

          <product-item :product="product" @del-item="removeProduct"></product-item>

        </div>
      </transition-group>
    </div>

    <product-select @sort-items="sortItems"></product-select>
  </div>
</template>

<script>
import ProductItem from './ProductItem.vue';
import ProductSelect from './ProductSelect.vue';

export default {
  props: ['products'],
  emits: ['delete', 'sort'],

  methods: {
    removeProduct(idx){
      this.$emit('delete', idx);
    },
    sortItems(value){
      this.$emit('sort', value)
    }
  },

  components: { ProductSelect, ProductItem }
}
</script>

<style>

</style>