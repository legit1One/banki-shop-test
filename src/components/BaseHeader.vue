<template>
    <div class="header">
        <div class="header__body">
            <ul class="header__links">
                <li class="header__link" v-for="link in links" :key="link">
                    {{ link }}
                </li>
            </ul>   

            <div class="header__search">
                <input v-model="search" type="text" placeholder="Поиск по названию картины">
                <BaseButton @click="$emit('search', search)" text="Найти"/>
            </div>
        </div>
    </div>
</template>
  
<script>
import BaseButton from './BaseButton.vue';

export default {
    name: 'BaseHeader',
    data: () => ({
        search: '',
        links: [
            'Каталог',
            'Доставка',
            'Оплата',
            'Контакты',
            'О компании',
        ]
    }),
    components: {
        BaseButton
    }
}
</script>
  
<style scoped lang="scss">
.header {
    width: 100vw;
    border-bottom: 1px solid #e1e1e1;
    padding: 24px 0;
    display: flex;
    justify-content: center;
    align-items: center;

    &__body {
        display: flex;
        justify-content: space-between;
        align-items: center;
        flex-wrap: wrap;
        width: 100%;
        max-width: 1120px;
        row-gap: 12px;
    }

    &__links {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-wrap: wrap;
        gap: 48px;
    }

    &__search {
        display: flex;
        align-items: center;

        input {
            height: 48px;
            border: 1px solid #e1e1e1;
            outline: none;
            padding: 0 16px;
            max-width: 298px;
            width: 100%;
            background: transparent;

            &::placeholder {
                color: #9F9F9F;
                font-size: 14px;
            }
        }
    }
}
    @media screen and (max-width: 640px) {
        .header {
            &__body {
                padding: 8px;
            }

            &__links, &__contacts {
                width: 100%;
                gap: 4px;
                justify-content: space-between;
            }

            &__search {
                width: 100%;
                margin-top: 12px;
            }
        }
    }
</style>
  