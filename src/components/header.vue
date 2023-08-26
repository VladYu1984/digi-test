<template>
    <div class="header-container">
        <div class="logo">
            <span>
                <img src="../assets/img/logo.svg" alt="логотип">
            </span>
            Логотип
        </div>
        <button class="btn btn-nav">Каталог</button>
        <div class="search">
            <span>
                <img src="../assets/img/search-icon.svg" alt="Иконка поиска">
            </span>
            <input type="text" class="input-head">
        </div>
        <ul>
            <li>Информация о компании</li>
            <li>Контакты</li>
            <li>Полезные ссылки</li>
        </ul>
    </div>
    <div class="header-container-mob">
        <div class="search-form">
            <span>
                <img src="../assets/img/arrow-right-mob.svg" alt="">
            </span>
            <div class="line-wrap">
                <input 
                    type="text" 
                    placeholder="Поиск..."
                    v-model="inputSearchMob"
                >
                <button class="clear-input-mob" @click="clearSearch">
                    <img src="../assets/img/search-clear.svg" alt="Очистить">
                </button>
                <button class="btn">Найти</button>
            </div>
        </div>
        <h1>Название категории</h1>
    </div>
</template>

<script>
export default {
    data() {
        return {
            inputSearchMob: ""
        }
    },
    methods: {
        clearSearch() {
            return this.inputSearchMob = "";
        },
    }
}
</script>

<style lang="scss" scoped>
    @import '../assets/styles/style.scss';
    .header-container {
        display: flex;
        padding: 12px 0;
        align-items: center;
        gap: 24px;

        @media (width <= 1000px) {
            display: none;
        }
    }

    .header-container-mob {
        display: none;
        @media (width <= 1000px) {
            display: block;

            &>.search-form {
                height: 53px;
                padding: 8px 16px 6px;
                display: flex;
                justify-content: flex-start;
                gap: 16px;
                align-items: center;

                &>.line-wrap {
                    display: flex;
                    width: 100%;
                    justify-content: space-between;
                    gap: 16px;
                    align-items: center;
                    height: 53px;
                    border-bottom: 1px solid $color-border;

                    &>span {
                        width: 20px;
                        height: 20px;
                    }

                    &>input {
                        width: 100%;
                        height: 100%;
                        font-size: $fz-16;

                        &:focus {
                            outline: none;
                        }
                    }
                }
            }

            &>h1 {
                padding: 0 24px;
                display: flex;
                justify-content: flex-start;
                margin: 12px 0;
                font-size: 22px;
                line-height: 28px;
            }
        }
        .clear-input-mob {
            background: none;
            border: none;
            padding: 0;
            cursor: pointer;
            display: flex;
            align-items: center;

            &:focus {
                outline: none;
            }

            img {
                opacity: .3;

                &:hover {
                opacity: 1;
                }
            }
        }
    }
    .btn-nav {
        width: 104px;
        height: 48px;
        margin-left: -16px;
        font-weight: 500;
        line-height: 16.94;
        color: #000;
    }

    span {
        display: flex;
        justify-content: center;
    }

    .logo {
        width: 145px;
        height: 48px;
        gap: 8px;
        padding: 0 24px;
        align-items: center;

        display: flex;
        justify-content: flex-start;
    }

    ul {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: flex-start;
        gap: 20px;

        @media( width <= 1110px) {
            display: none;
        }
    }

    .input-head {
        height: 100%;
        width: 100%;
        &:focus {
            outline: none;
        }
    }
</style>