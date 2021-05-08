<template>
    <div class="search-wrapper">
        <form class="flex ai-center">
            <label for="search">Search by {{searching}}:</label>
            <div class="search-bar">
                <input v-model="searchText" type="text" name="search" id="search" :placeholder="`Search ${searching}`">
                <i class="fas fa-times" @click="reset"></i>
            </div>
            <button type="submit" @click.prevent="send"><i class="fas fa-search"></i></button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'Search',
    props:{
        searching: String,
    },
    data(){
        return{
            searchText: '',
        }
    },
    methods:{
        /**
         * Send search
         */
        send(){
            this.$emit(`${this.searching}Search`, this.searchText);           
            this.searchText = '';
        },
        /**
         * Clean search input
         */
        reset(){
            this.searchText = '';
        }
    }
}
</script>

<style scoped lang="scss">
    .search-wrapper{
        margin: 10px;
        flex-shrink: 0;

        .search-bar{
            position: relative;
            margin-left: 15px;
            
            input{
                padding: 5px 25px 5px 10px;
            }

            i{
                position: absolute;
                top: 50%;
                right: 10px;
                transform: translateY(-50%);
                font-size: 1.2rem;
                color: #aaa;
                cursor: pointer;
                transition: color .2s;

                &:hover{
                    color: #ddd;
                }
            }

        }

        button{
            width: 40px;
            align-self: stretch;
        }
    }
</style>