<template>
    <div class="filters flex ai-center">
        <div class="title" @click="toggle">
            <i v-show="!isVisible" class="fas fa-plus"></i>
            <i v-show="isVisible" class="fas fa-minus"></i> 
            filters
        </div>
        <!-- Filters -->
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
        margin-right: 10px;
        font-size: 1.5em;
        text-transform: uppercase;
        cursor: pointer;
    }
    .filters-container{
        width: 100%;
        height: 100%;
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

    // Media Query
    @media screen and (max-width: $md){
        .filters,
        .filters-container{
            flex-direction: column;
        }
        .filters-container.hidden{
            width: 100%;
            padding: 0 20px;

            height: 0;
        }
    }
</style>