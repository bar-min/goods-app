<template>
  <main class="blocks">
    <div class="blocks__container blocks-wrapper">

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
            <label for="link" class="label-menu label-menu-required">Наименование товара</label>
            <input v-model="link" @blur="checkInput" class='input-menu' id="link" placeholder="Введите ссылку">
          </div>
          <div class="menu__price" :class="{'menu-required': !isValidPrice }">
            <label for="price" class="label-menu label-menu-required">Цена товара</label>
            <input v-model="validPrice" @blur="checkInput" class='input-menu' id="price" placeholder="Введите цену">
          </div>
        </div>
        <button class="menu__btn" :class="{'menu__btn_active': isValid}" :disabled="isValid">Добавить товар</button>
      </div>

      <div class="products">
        <div class="products__container">
          <div class="products__card card" v-for="item in 9" :key="item">
            
            <div class="card__picture">
              <img src="@/assets/images/item-default.png" alt="product">
            </div>

            <div class="card__body">
              <h3 class="card__title">Наименование товара</h3>

              <p class="card__text">Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк</p>

              <span class="card__price">10 000 руб.</span>
            </div>

            <div class="card__remove"></div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: 'App',
  data(){
    return {
      isValidTitle: true,
      isValidLink: true,
      isValidPrice: true,
      title: '',
      description: '',
      link: '',
      price: ''
    }
  },
  
  computed: {
    isValid(){
     return (this.title && this.link && this.price) ? true : false;
    },
    
    validPrice:{
      get(){
        return this.price.toLocaleString();
      }, 
      set(value){
        this.price = +value.replace(/\s/g, "");
      }
    },
  },

  methods: {
    checkInput(){
      this.isValidTitle = (!this.title) ? false : true; 
      this.isValidLink = (!this.link) ? false : true; 
      this.isValidPrice = (!this.price) ? false : true; 
    }
  },

  components: {},
}
</script>

<style>
</style>
