<template>
   <div class="overlay" @click.self="$emit('close')">
        <div class="modal" @click.stop>
            <swiper-container
                :slides-per-view="1"
            >
                <swiper-slide><img :src="item.image" alt="image"></swiper-slide>
                <swiper-slide><img :src="item.image" alt="image"></swiper-slide>
                <swiper-slide><img :src="item.image" alt="image"></swiper-slide>
            </swiper-container>
            <div class="modal__body">
                <div class="modal__description">
                    {{ item.description }}
                </div>

                <div class="modal__price">
                    {{ item.price ? `${item.price?.toLocaleString()} $` : 'Продано на аукционе' }} 
                </div>
            </div>
        </div>
   </div>
</template>

<script>

export default {
    name: 'CardModal',
    props: {
        item: {
            type: Object,
            required: true
        },
    },
}
</script>

<style lang="scss">
    .overlay {
        position: fixed;
        top: 0;
        left: 0;
        width: 100vw;
        height: 100vh;
        background: rgba(0, 0, 0, 0.5);
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .modal {
        background: #fff;
        max-width: 480px;
        width: calc(100% - 24px);

        img {
            width: 100%;
        }

        &__body {
            padding: 16px;
        }

        &__description {
            font-size: 20px;
            font-weight: 700;
            margin-bottom: 20px;
        }

        &__price {
            font-size: 18px;
            font-weight: 700;
        }
    }
</style>