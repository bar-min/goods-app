<template>
  <main class="blocks">
    <div class="blocks__container blocks-wrapper">
      <pro-loader :loading="loading"></pro-loader>
      
      <add-menu @add="addProduct"></add-menu>

      <product-list @delete="deleteProduct" @sort="sortProducts" :products="products"></product-list>

      <add-modal :show="added"></add-modal>
    </div>
  </main>
</template>

<script>
import AddMenu from './components/AddMenu.vue';
import AddModal from './components/AddModal.vue';
import ProductList from './components/ProductList.vue';
import ProLoader from './components/ProLoader.vue';

import defaultPicture from './assets/images/item-default.png';

export default {
  name: 'App',

  data(){
    return {
      products: [],
      selected: '',
      added: false,
      loading: false
    }
  },

  product: {title: 'Наименование товара', 
            description: `Довольно-таки интересное описание товара в несколько строк. 
            Довольно-таки интересное описание товара в несколько строк`, 
            url: defaultPicture, 
            price: 10000},

  mounted(){
    this.getProducts();
  },

  methods: {
    addProduct(value){
      this.products.push(value);

      this.showModal();

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
    setDefaultProducts(){
      let product = this.$options.product;
      this.products = Array.from(Array(9).keys()).map(idx => {
        return { ...product, id: idx}
      })
    },
    getProducts(){
      // Simulate a request to the server (for loading)
      let response = new Promise(((resolve, reject) => {
        this.loading = true;

        let allProducts = localStorage.getItem('products');

        if(!allProducts){
          setTimeout(() => reject(), 500)
        }

        setTimeout(() => resolve(allProducts), 500)
      }))

      response
      .then(data => {
        this.products = JSON.parse(data);
      })
      .catch(() => {
        this.setDefaultProducts();
      })
      .finally(() => {
        setTimeout(() => { this.loading = false }, 1000)
      })
    },
    showModal(){
      this.added = true;
      setTimeout(() => {
        this.added = false;
      }, 3000)
    }
  },

  components: { AddMenu, AddModal, ProductList, ProLoader },
}
</script>

<style>
</style>
