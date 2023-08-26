<template>
    <div class="left">
        <div class="custom-dropdown">
            <div class="selected-option" @click="toggleDropdown">
                <span class="arrow" :class="{ 'open': isDropdownOpen }">
                    <img src="../assets/img/arrow-right.svg" alt="стрелка открыть меню" class="arrow-icon">
                </span>
                {{ 'Выбранные категории' }}
            </div>
            <div v-if="isDropdownOpen" class="options">
                <div
                    v-for="(option, index) in options"
                    :key="index"
                    @click="toggleSelected(index)"
                    :class="{ 'option': true, 'active': isSelected(index) }"
                >
                    {{ option }} <span>3</span>
                </div>
            </div>
        </div>
        <div class="slider-filter">
            <p>Цена</p>
            <div class="price-range">
                <input
                    type="text"
                    placeholder="от"
                    v-model="numericValueFrom" @input="validateNumericInput"
                >
                —
                <input 
                    type="text"
                    placeholder="до"
                    v-model="numericValueTo" @input="validateNumericInput"
                >
            </div>
        </div>

        <div class="checkbox-filter-brand">
            <p>
                Бренд
                <button 
                    class="clear"
                    @click="clearSelection"
                >Очистить</button>
            </p>
            <div class="search-brand">
                <span>
                    <img src="../assets/img/search-brand.svg" alt="Иконка поиска">
                </span>
                <input type="text" placeholder="Поиск"
                v-model="searchInput">
                <button 
                  class="clear-input" @click="clearSearch"
                >
                    <img src="../assets/img/search-clear.svg" alt="Очистить">
                </button>
            </div>
            <div class="checkbox-list">
                <ul>
                    <li v-for="checkbox in 11" :key="checkbox">
                        <input type="checkbox">
                        Атрибут
                        <span>3</span>
                    </li>
                </ul>
            </div>
        </div>
        <div class="checkbox-filter-size">
            <p>Размер</p>
            <div class="checkbox-list">
                <ul>
                    <li v-for="checkbox in 9" :key="checkbox">
                        <input type="checkbox" name="" id="">
                        Атрибут<span>3</span>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            isDropdownOpen: false,
            selectedOptions: [],
            selectedOption: null,
            numericValueFrom: "",
            numericValueTo: "",
            searchInput: "",
            options: [
                'Название категории',
                'Название категории',
                'Название категории',
            ],
        };
    },
    methods: {
        toggleDropdown() {
            this.isDropdownOpen = !this.isDropdownOpen;
        },
        toggleSelected(index) {
            if (this.selectedOptions[index]) {
                this.selectedOptions[index] = false;
            } else {
                this.selectedOptions[index] = true;
            }
        },
        isSelected(index) {
            return this.selectedOptions[index];
        },
        validateNumericInput() {
            this.numericValueFrom = this.numericValueFrom.replace(/[^\d.]/g, "");
            this.numericValueTo = this.numericValueTo.replace(/[^\d.]/g, "");

            const decimalCountFrom = (this.numericValueFrom.match(/\./g) || []).length;
            const decimalCountTo = (this.numericValueTo.match(/\./g) || []).length;

            if (decimalCountFrom > 1 || decimalCountTo > 1) {
                this.numericValueFrom = this.numericValueFrom.replace(/\.+$/, "");
                this.numericValueTo = this.numericValueTo.replace(/\.+$/, "");
            }
            if (this.numericValueFrom !== "" || this.numericValueTo !== "") {
                this.numericValueFrom += " ₽";
                this.numericValueTo += " ₽";
            }
        },
        clearSelection() {
            return this.selectedOptions = []
        },
        clearSearch() {
            return this.searchInput = "";
        },
    },
};
</script>

<style lang="scss" scoped>
@import '../assets/styles/style.scss';

.custom-dropdown {
    position: relative;
    display: inline-block;
    width: 280px;
    margin-bottom: 90px;
}

.selected-option {
    cursor: pointer;
    padding: 10px;
    height: 30px;
    padding: 0 16px 0 8px;
    color: $color-font-main;
    display: flex;
    align-items: center;
}

.options {
    position: absolute;
    top: 100%;
    left: 0;
    width: 100%;
    z-index: 1;
}

.option {
    padding: 0 16px 0 32px;
    height: 30px;
    cursor: pointer;
    transition: background-color 0.2s;
    display: flex;
    align-items: center;
    justify-content: space-between;
    color: $color-font-main;

    &:hover {
        color: $color-brand;
    }
    &>span {
        color: $color-font-second;

    }
}

.arrow {
    transition: transform 0.2s;
    display: inline-flex;
    line-height: $lh-16;
}

.selected-option.open {
    .arrow {
        transform: rotate(180deg);
    }
}

.arrow-icon {
    width: 16px;
    height: 16px;
    transition: transform 0.4s ease;
}

.arrow.open .arrow-icon {
    transform: rotate(-90deg);
}

.slider-filter {
    &>p {
        line-height: 1.25 * $lh-16;
        font-weight: $fw-700;
        justify-content: center;
        display: flex;
        color: $color-font-main;
        margin-bottom: 16px;
    }

    &>.price-range {
        display: flex;
        justify-content: space-around;
        align-items: center;
        gap: 16px;
        align-self: stretch;
        border-radius: 4px;
        height: 36px;
        color: $color-font-second;

        &>input {
            width: 100%;
            height: 100%;
            border-radius: 4px;
            border: 1px solid $color-border;
            padding: 10px 8px;

            &:focus {
                border-color: $color-brand;
                outline: none;
            }
        }
    }
}

.checkbox-filter-brand {
    gap: 16px;
    display: flex;
    flex-direction: column;

    &>p {
        display: flex;
        justify-content: space-between;
        line-height: 1.25 * $lh-16;
        font-weight: $fw-700;
        color: $color-font-main;
        margin-bottom: 16px;

        &>button {
            background: none;
            text-decoration: underline;
            color: $color-font-second;
            font-size: $fz-12;
            line-height: 12px;
            cursor: pointer;
        }
    }

    &>.search-brand {
        display: flex;
        align-items: center;
        gap: 8px;
        padding: 10px 12px;
        border: 1px solid $color-font-second;
        border-radius: 4px;

        &>span {
            color: $color-font-second;
        }

        &>input {
          width: 100%;
            &:focus {
                outline: none;
            }
        }

        &:hover {
            border-color: $color-brand;
        }
    }

    // &>.checkbox-list {
        
    // }
}

.checkbox-list{
    max-height: 180px; 
    overflow-y: auto;
    list-style: none;
    padding: 0;
    margin: 0;
    position: sticky;
    top: 0;

    &> ul {
        display: flex;
        gap: 12px;
        flex-direction: column;

        &>li {
            cursor: pointer;
            padding-right: 16px;
            height: 20px;
            font-family: $ff-sec;
            color: $color-font-main;
            border-radius: 5px;
            font-size: $fz-16;
            display: flex;
            align-items: center;
            gap: 12px;

            &>span {
                display: flex;
                margin-left: auto;
            }

            &>input {
                width: 20px;
                height: 20px;
            }

            &>span {
                color: $color-font-second;
            }
        }
    }
}

.checkbox-filter-size {
    &>p {
        margin-bottom: 16px;
    }
}

.clear-input {
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
        width: 16px;
        height: 16px;
        opacity: .3;

        &:hover {
          opacity: 1;
        }
    }
}
</style>