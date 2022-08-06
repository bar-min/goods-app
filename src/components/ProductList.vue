<template>
  <div class="products">
    <div class="products__container">
      <div class="products__card card" v-for="product in products" :key="product.title">

        <div class="card__picture">
          <img :src="product.url" alt="product">
        </div>

        <div class="card__body">
          <h3 class="card__title"></h3>

          <p class="card__text">{{ product.description }}</p>

          <span class="card__price">{{ validPrice(product.price) }}</span>
        </div>

        <div @click="deleteProduct(product.id)" class="card__remove"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['products'],
  emits: ['delete'],

  computed: {
    validPrice(){
      return (price, currency = 'руб.') => price.toLocaleString() + ' ' + currency;
    }
  },

  methods: {
    deleteProduct(idx){
      this.$emit('delete', idx);
    }
  }
}
</script>

<style>

</style>