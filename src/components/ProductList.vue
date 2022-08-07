<template>
  <div class="products">
    <div class="products__container">
      <transition-group name="list">
        <div class="products__card card" v-for="product in products" :key="product.id">
  
          <div class="card__picture">
            <img :src="product.url" alt="product" @error="checkImage">
          </div>

          <div class="card__body">
            <h3 class="card__title">{{ product.title }}</h3>

            <p class="card__text">{{ product.description }}</p>

            <span class="card__price">{{ validPrice(product.price) }}</span>
          </div>

          <div @click="deleteProduct(product.id)" class="card__remove"></div>
        </div>
      </transition-group>
    </div>

    <div class="products__select">
      <select class="select"  @change="$emit('sort', $event.target.value)">
        <option selected disabled>По умолчанию</option>
        <option value="name">По названию</option>
        <option value="max">По цене max</option>
        <option value="min">По цене min</option>
      </select>
    </div>

  </div>
</template>

<script>
export default {
  props: ['products'],

  emits: ['delete', 'sort'],

  computed: {
    validPrice(){
      return (price, currency = 'руб.') => {
        return price.toLocaleString() + ' ' + currency;
      }
    }
  },

  methods: {
    deleteProduct(idx){
      this.$emit('delete', idx);
    },

    checkImage(event){
      let picture = event.target.closest('.card__picture');
      picture.style.display = 'none';
    }
  }
}
</script>

<style>

</style>