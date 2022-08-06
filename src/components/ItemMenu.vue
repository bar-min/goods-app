<template>
  <div class="menu">
    <div class="menu__body">
      <h2 class="menu__heading">Добавление товара</h2>
      
      <div class="menu__title" :class="{'menu-required': !isValidTitle }">
        <label for="title" class="label-menu label-menu-required">Наименование товара</label>
        <input v-model="title" @blur="checkInput" class='input-menu' id="title" placeholder="Введите наименование товара">
      </div>

      <div class="menu__description">
        <label for="area" class="label-menu">Описание товара</label>
        <textarea v-model="description" class='input-menu' id="area" placeholder="Введите описание товара"></textarea>
      </div>

      <div class="menu__link" :class="{'menu-required': !isValidLink }">
        <label for="link" class="label-menu label-menu-required">Ссылка на изображение товара</label>
        <input v-model="url" @blur="checkInput" class='input-menu' id="link" placeholder="Введите ссылку">
      </div>

      <div class="menu__price" :class="{'menu-required': !isValidPrice }">
        <label for="price" class="label-menu label-menu-required">Цена товара</label>
        <input :value="price" @input="checkPrice" @blur="checkInput" class='input-menu' id="price" placeholder="Введите цену">
      </div>
    </div>

    <button 
    @click="addProduct" 
    class="menu__btn" 
    :class="{'menu__btn_active': isValid}" 
    :disabled="!isValid">Добавить товар</button>
  </div>
</template>

<script>
export default {
  data(){
    return {
      isValidTitle: true,
      isValidLink: true,
      isValidPrice: true,
      title: '',
      description: '',
      url: '',
      price: '',
      id: Date.now()
    }
  },
  
  emits: ['add'],

  computed: {
    isValid(){
      return (this.title && this.url && this.price) ? true : false;
    },
    newProduct(){
      return { title: this.title, description: this.description, url: this.url, price: this.price, id: this.id }
    },
  },
  methods: {
    checkPrice(event){
      const inputValue = event.target.value.replace(/\s/g, "");

      if(isNaN(inputValue) || inputValue == ''){
        event.target.value = this.price;
      } else {
        this.price = (+inputValue).toLocaleString();
      }
    },
    addProduct(){
      this.$emit('add', this.newProduct)
      this.clearInputs();
    },
    
    clearInputs(){
      this.title = '';
      this.description = '';
      this.url = '';
      this.price = '';
      this.id = '';
    },

    checkInput(){
      this.isValidTitle = (!this.title) ? false : true; 
      this.isValidLink = (!this.url) ? false : true; 
      this.isValidPrice = (!this.price) ? false : true; 
    },
  }
}
</script>

<style>

</style>