<template>
    <div class="card" :class="{ 'card--disabled': item.disabled }">
        <img :src="item.image" alt="item image" @click="$emit('openInfo')">

        <span class="card__title" @click="$emit('openInfo')">{{ item.title }}</span>

        <div class="card__footer">
            <template v-if="!item.disabled">
                <div>
                    <div class="card__price card__price--old" v-if="item.oldPrice !== undefined">
                        {{ item.oldPrice?.toLocaleString() }} $
                    </div>
                    <div class="card__price"  v-if="item.oldPrice !== null">
                        {{ item.price?.toLocaleString() }} $
                    </div>
                </div>

                <BaseButton @click="purchaseItem"
                            :loading="loading" :text="isInCart ? 'В корзине' : 'Купить'" 
                            :color="isInCart ? 'lightbrown' : 'darkbrown'"
                >
                    <template #icon v-if="isInCart">
                        <img src="@/assets/checked.svg" alt="checked">
                    </template>
                </BaseButton>
            </template>

            <div class="card__sold" v-else>
                Продана на аукционе
            </div>
        </div>
    </div>
</template>
  
<script>
import BaseButton from './BaseButton.vue';
export default {
    name: 'ItemCard',
    data: () => ({
        loading: false,
    }),
    props: {
        item: {
            type: Object,
            required: true
        }
    },
    components: {
        BaseButton
    },
    methods: {
        purchaseItem() {
            this.loading = true
            setTimeout(() => {
                const index = this.$parent.$parent.$data.cart.findIndex(item => item.id === this.item.id)
                if(index === -1) {
                    this.$parent.$parent.$data.cart.push(this.item)
                } else {
                    this.$parent.$parent.$data.cart.splice(index, 1)
                }

                this.loading = false
            }, 2000)
        }
    },
    computed: {
        isInCart() {
            return this.$parent.$parent.$data.cart.some(item => item.id === this.item.id)
        }
    }
}
</script>

<style scoped lang="scss">
.card {
    display: flex;
    flex-direction: column;
    max-width: 280px;
    border: 1px solid #e1e1e1;

    &--disabled {
        opacity: .5;
    }

    &__title {
        font-size: 18px;
        line-height: 27px;
        max-width: 220px;
        margin: 20px auto 0;
    }

    &__footer {
        padding: 24px;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    &__price {
        font-weight: 700;
    }

    &__price--old {
        font-size: 14px;
        color: #A0A0A0;
        text-decoration: 1px line-through;
        line-height: 21px;
    }

    &__sold {
        font-weight: 700;
    }
}
</style>
  