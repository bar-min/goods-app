<template>
  <main class="blocks">
    <div class="blocks__container blocks-wrapper">

      <div class="menu">
        <div class="menu__body">
          <h2 class="menu__heading">Добавление товара</h2>
          <div class="menu__title">
            <label for="title" class="label-menu label-menu-required">Наименование товара</label>
            <input class='input-menu' id="title" placeholder="Введите наименование товара">
          </div>
          <div class="menu__description">
            <label for="area" class="label-menu">Описание товара</label>
            <textarea class='input-menu' id="area" placeholder="Введите описание товара"></textarea>
          </div>
          <div class="menu__link">
            <label for="link" class="label-menu label-menu-required">Наименование товара</label>
            <input class='input-menu' id="link" placeholder="Введите ссылку">
          </div>
          <div class="menu__price">
            <label for="link" class="label-menu label-menu-required">Цена товара</label>
            <input class='input-menu' id="link" placeholder="Введите цену">
          </div>
        </div>
        <button class="menu__btn">Добавить товар</button>
      </div>

      <div class="products">
        <div class="products__container">
          <div class="products__card card" v-for="item in 6" :key="item">
            
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
  components: {}
}
</script>

<style lang="scss">
</style>
