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

      <div class="products"></div>
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
