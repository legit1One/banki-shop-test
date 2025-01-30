<template>
  <div id="app">
    <BaseHeader @search="search = $event"/>
    <div class="main">
      <Category v-for="category in filteredCategories" :category="category" :key="category.title" @openInfo="itemToShow = $event" />

      <div class="notfound" v-if="!filteredCategories.length">
        Ничего не найдено
      </div>
    </div>

    <BaseModal v-if="itemToShow" @close="itemToShow = null" :item="itemToShow"></BaseModal>
    <BaseFooter />
  </div>
</template>

<script>
import BaseHeader from './components/BaseHeader.vue';
import BaseFooter from './components/BaseFooter.vue';
import BaseModal from './components/CardModal.vue';
import Category from './components/Category.vue';

export default {
  name: 'App',
  data: () => ({
    search: '',
    itemToShow: null,
    categories: [{
      title: 'Картины эпохи Возрождения',
      items: [
        {
          id: 1,
          title: '«Рождение Венеры» Сандро Боттичелли',
          description: '«Рождение Венеры» Сандро Боттичелли, «Тайная вечеря»  Леонардо да Винчи',
          oldPrice: 2000000,
          price: 1000000,
          disabled: false,
          image: require('@/assets/painting-1.svg')
        },
        {
          id: 2,
          title: '«Тайная вечеря»  Леонардо да Винчи',
          description: '«Рождение Венеры» Сандро Боттичелли, «Тайная вечеря»  Леонардо да Винчи',
          price: 3000000,
          disabled: false,
          image: require('@/assets/painting-2.svg')
        },
        {
          id: 3,
          title: '«Сотворение Адама» Микеланджело',
          description: '«Рождение Венеры» Сандро Боттичелли, «Тайная вечеря»  Леонардо да Винчи',
          oldPrice: 6000000,
          price: 5000000,
          disabled: false,
          image: require('@/assets/painting-3.svg')
        },
        {
          id: 4,
          title: '«Урок анатомии»  Рембрандт',
          description: '«Рождение Венеры» Сандро Боттичелли, «Тайная вечеря»  Леонардо да Винчи',
          oldPrice: null,
          price: null,
          disabled: true,
          image: require('@/assets/painting-4.svg')
        },
      ]
    }]
  }), 
  components: {
    BaseHeader,
    BaseFooter,
    BaseModal,
    Category
  },
  computed: {
    filteredCategories() {
      if(!this.search) return this.categories

      return this.categories.map(category => {
        return {
          ...category,
          items: category.items.filter(item => {
            return item.title.toUpperCase().includes(this.search.toUpperCase())
          })
        }
      }).filter(category => category.items.length)
    }
  }
}
</script>

<style lang="scss">
@import url('./assets/main.scss');

#app {
  display: flex;
  flex-direction: column;
}

.main {
  min-height: calc(100vh - 194px);
  max-width: 1216px;
  margin: auto;
  padding-bottom: 24px;
}

.notfound {
    margin-top: 40px;
    font-weight: 700;
}
</style>
