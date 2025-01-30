<template>
    <div class="footer">
        <div class="footer__body">
            <ul class="footer__links">
                <li class="footer__link" v-for="link in links" :key="link">
                    {{ link }}
                </li>
            </ul>   

            <div class="footer__contacts">
                <p>
                    <img src="@/assets/phone.svg" alt="phone">
                    +7 (812) 555-55-55
                </p>
                <p>
                    <img src="@/assets/location.svg" alt="location">
                    г. Санкт-Петербург, ул. Ефимова, 3
                </p>
            </div>
        </div>
    </div>
</template>
  
<script>

export default {
    name: 'BaseFooter',
    data: () => ({
        links: [
            'Каталог',
            'Доставка',
            'Оплата',
            'Контакты',
            'О компании',
        ]
    })
}
</script>
  
<style scoped lang="scss">
.footer {
    width: 100vw;
    min-height: 96px;
    display: flex;
    justify-content: center;
    align-items: center;
    background: #eceaea;
    color: #555555;
    font-size: 14px;
    line-height: 21px;
    padding: 0 40px;

    &__body {
        display: flex;
        justify-content: space-between;
        align-items: center;
        width: 100%;
        max-width: 1120px;
        flex-wrap: wrap;
        row-gap: 12px ;
    }

    &__links {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-wrap: wrap;
        gap: 48px;
    }


    &__contacts {
        display: flex;
        align-items: center;
        flex-wrap: wrap;
        gap: 51px;
        
        p {
            display: flex;
            align-items: center;
            gap: 2px;
        }
    }

    @media screen and (max-width: 620px) {
        .footer {
            &__body {
                padding: 8px;
            }

            &__links, &__contacts {
                width: 100%;
                gap: 4px;
                justify-content: space-between;
            }
        }
    }
}
</style>
  