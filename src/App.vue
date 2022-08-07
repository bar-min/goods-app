<template>
  <main class="blocks">
    <div class="blocks__container blocks-wrapper">
      <add-menu @add="addProduct"></add-menu>

      <product-list @delete="deleteProduct" @sort="sortProducts" :products="products"></product-list>

      <add-modal :show="added"></add-modal>
    </div>
  </main>
</template>

<script>
import AddMenu from './components/AddMenu.vue';
import ProductList from './components/ProductList.vue';
import AddModal from './components/AddModal.vue';
import defaultPicture from './assets/images/item-default.png';

export default {
  name: 'App',
  data(){
    return {
      products: [],
      selected: '',
      added: false
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

    getProducts(){
      let allProducts = localStorage.getItem('products');

      if(!allProducts){
        return;
      }
      
      this.products = JSON.parse(allProducts);
    },

    showModal(){
      this.added = true;
      setTimeout(() => {
        this.added = false;
      }, 3000)
    }
  },

  components: { AddMenu, ProductList, AddModal },
}
</script>

<style>
</style>
