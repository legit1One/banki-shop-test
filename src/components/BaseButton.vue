<template>
    <button class="button" :disabled="loading" :class="getColorClass()" @click="$emit('click')">
        <div class="button__icon">
            <img src="@/assets/loader.svg" alt="loader" class="loader" v-if="loading">
            <slot name="icon" v-else></slot>
        </div>
        {{ text }}
    </button>
  </template>
  <script>
  
  export default {
    name: 'BaseButton',
    props: {
        loading: {
            type: Boolean,
            default: false
        },
        color: {
            type: String,
            default: 'darkbrown',
            validator: (value) => ['darkbrown' , 'lightbrown', 'mediumbrown'].includes(value)
        },
        text: {
            type: String,
            required: true
        }
    },
    methods: {
        getColorClass() {
            if(this.loading) return 'button--gray'

            return `button--${this.color}`
        }
    }
  }
  </script>
  
  <style scoped lang="scss">
  .button {
    display: flex;
    align-items: center;
    justify-content: center;
    color: #F4F6F9;
    width: 118px;
    height: 48px;
    cursor: pointer;
    font-size: 14px;
    outline: none;
    border: none;

    &--darkbrown {
        background: #382E2B;
    }

    &--lightbrown {
        background: #5B3A32;
    }

    &--gray {
        background: #4d4949;
    }

    &__icon {
        display: flex;
        margin-right: 4px;
    }
  }

  .loader {
    width: 20px;
    height: 20px;
    animation: rotate 1s ease-in-out infinite;

    @keyframes rotate {
        100% {
            transform: rotate(360deg);
        }
    }
  }
  </style>
  