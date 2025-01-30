<template>
    <div v-if="category.title" class="category">
          <h3 class="category__title">{{ category.title }}</h3>

          <div class="category__items">
            <ItemCard v-for="item in category.items" :key="item.id" :item="item" @openInfo="$emit('openInfo', item)"/>  
          </div>
      </div>
</template>
<script>
import ItemCard from './ItemCard.vue';

export default {
    name: 'CategoryBlock',
    props: {
        category: {
            type: Object,
            required: true
        }
    },
    components: {
        ItemCard
    }
}
</script>

<style lang="scss" scoped>

.category {
  &__title {
    font-size: 24px;
    font-weight: 700;
    line-height: 36px;
    margin-top: 45px;
    margin-bottom: 39px;
    @media screen and (max-width: 1216px) {
      & {
        text-align: center;
      }
    }
  }
  
  &__items {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 32px;

    &--empty {
      margin-top: 40px;
      font-weight: 700;
    }
  }
}
</style>