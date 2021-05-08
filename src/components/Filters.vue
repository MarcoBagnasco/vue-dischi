<template>
    <div class="filters flex">
        <div class="title">
            <i v-show="!isVisible" class="fas fa-plus" @click="toggle"></i>
            <i v-show="isVisible" class="fas fa-minus" @click="toggle"></i> 
            filters
        </div>
        <div class="filter-container-wrapper">
            <div class="filters-container flex ai-center"  :class="{hidden: !isVisible}">
                <slot></slot>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Filters',
    data(){
        return{
            isVisible: false,
        }
    },
    methods: {
        /**
         * Toggle filters visibility
         */
        toggle(){
            this.isVisible = !this.isVisible;
        }
    }
}
</script>

<style scoped lang="scss">
// VARIABLES SCSS
@import '@/styles/variables.scss';

    .title{
        margin-right: 30px;
        font-size: 2.5rem;
        text-transform: uppercase;

        i{
            cursor: pointer;
        }
    }
    .filters-container{
        width: 100%;
        padding: 0 20px;
        background-color: $bg-elements;
        overflow: hidden;
        transition: width .2s linear,
                    padding .1s .1s linear;

        &.hidden{
            width: 0;
            padding: 0;
        }
    }
</style>