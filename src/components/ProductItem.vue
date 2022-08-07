<template>
  <div class="card__picture">
    <img :src="product.url" alt="product" @error="checkImage">
  </div>

  <div class="card__body">
    <h3 class="card__title">{{ product.title }}</h3>

    <p class="card__text">{{ product.description }}</p>

    <span class="card__price">{{ validPrice(product.price) }}</span>
  </div>

  <div @click="$emit('del-item', product.id)" class="card__remove"></div>
</template>

<script>
export default {
  props: ['product'],
  emits: ['del-item'],

  computed: {
    validPrice(){
      return (price, currency = 'руб.') => {
        return price.toLocaleString() + ' ' + currency;
      }
    }
  },

  methods: {
    checkImage(event){
      let picture = event.target.closest('.card__picture');
      picture.style.display = 'none';
    },
  }
}
</script>

<style>

</style>