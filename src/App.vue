<template>
  <main class="blocks">
    <div class="blocks__container blocks-wrapper">
      <item-menu @add="addProduct"></item-menu>

      <product-list @delete="deleteProduct" :products="products"></product-list>
    </div>
  </main>
</template>

<script>
import ItemMenu from './components/ItemMenu.vue';
import ProductList from './components/ProductList.vue';
import defaultPicture from './assets/images/item-default.png';

export default {
  name: 'App',
  data(){
    return {
      products: []
    }
  },

  product: {title: 'Наименование товара', 
            description: `Довольно-таки интересное описание товара в несколько строк. 
            Довольно-таки интересное описание товара в несколько строк`, 
            url: defaultPicture, 
            price: 10000},

  beforeMount(){
    let product = this.$options.product;
    this.products = Array.from(Array(9).keys()).map(idx => {
      return { ...product, id: idx}
    })
  },

  methods: {
    addProduct(value){
      this.products.push(value);
    },

    deleteProduct(idx){
      let current = this.products.findIndex(item => item.id === idx);
      this.products.splice(current, 1);
    }
  },

  components: { ItemMenu, ProductList },
}
</script>

<style>
</style>
