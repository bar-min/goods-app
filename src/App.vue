<template>
  <main class="blocks">
    <div class="blocks__container blocks-wrapper">
      <item-menu @add="addProduct"></item-menu>

      <product-list @delete="deleteProduct" @sort="sortProducts" :products="products"></product-list>
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
      products: [],
      selected: '',
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

  mounted(){
    this.getProducts();
  },

  methods: {
    addProduct(value){
      this.products.push(value);

      if(this.selected) this.sortProducts(this.selected);

      this.saveProducts();
    },

    deleteProduct(idx){
      let current = this.products.findIndex(item => item.id === idx);
      this.products.splice(current, 1);

      this.saveProducts();
    },

    sortProducts(option){
      this.selected = option;
      switch(this.selected){
        case 'min': 
          this.products.sort((a, b) => a.price - b.price);
          break;
        case 'max':
          this.products.sort((a, b) => b.price - a.price);
          break;
        case 'name':
          this.products.sort((a, b) => a.title.localeCompare(b.title));
          break;
      }
    },

    saveProducts(){
      localStorage.setItem('products', JSON.stringify(this.products));
    },

    getProducts(){
      let allProducts = localStorage.getItem('products');

      if(!allProducts){
        return;
      } 
      else if(!JSON.parse(allProducts).length){
        return;
      }
      
      this.products = JSON.parse(allProducts);
    }
  },

  components: { ItemMenu, ProductList },
}
</script>

<style>
</style>
