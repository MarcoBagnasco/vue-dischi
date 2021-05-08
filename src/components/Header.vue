<template>
    <header>
        <img src="../assets/img/logo.png" alt="logo">
    </header>
</template>

<script>
export default {
    name: 'Header',
}
</script>

<style scoped lang="scss">
// VARIABLES SCSS
@import '@/styles/variables.scss';

    header{
        height: 65px;
        padding: 10px;
        background-color: $bg-elements;

        img{
            height: 100%;
        }
    }
</style>