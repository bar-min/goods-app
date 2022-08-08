<template>
  <div class="card__picture">
    <img :src="validPicture(product.url)" alt="product" @error="checkImage">
  </div>

  <h3 class="card__title">{{ product.title }}</h3>

  <p class="card__text">{{ product.description }}</p>
  
  <div class="card__price">{{ validPrice(product.price) }}</div>

  <div @click="$emit('del-item', product.id)" class="card__remove"></div>
</template>

<script>
import unkImage from '@/assets/images/unknown-picture.jpg';

export default {
  props: ['product'],
  emits: ['del-item'],

  data(){
    return {
      unkImage,
      loadImage: true
    }
  },

  computed: {
    validPrice(){
      return (price, currency = 'руб.') => {
        return price.toLocaleString() + ' ' + currency;
      }
    },
    validPicture(){
      return (url) => { 
        if(this.loadImage){
          return url;
        } else {
          return this.unkImage;
        }
      }
    }
  },

  methods: {
    checkImage(){
      this.loadImage = false;
    },
  }
}
</script>

<style>

</style>