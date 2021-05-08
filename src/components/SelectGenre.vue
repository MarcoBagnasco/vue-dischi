<template>
    <div class="select flex ai-center">
        <label for="genre">Filter by genre:</label>
        <select name="genre" id="genre" v-model="option" @change="$emit('selection', option)">
            <option value="all">All</option>
            <option v-for="(item, index) in getGenre" :key="index" :value="item.toLowerCase()">{{item}}</option>
        </select>
    </div>
</template>

<script>
export default {
    name: 'SelectGenre',
    props: {
        genre: Array,
        option: String,
    },
    data(){
        return {
            genreList : [],
        }
    },
    computed: {
        /**
         * Populate genre's array
         */
        getGenre(){
            this.genre.forEach(item => {
                if(!this.genreList.includes(item.genre)){
                    this.genreList.push(item.genre)
                }
            });
            return this.genreList
        }
    },
}
</script>

<style scoped lang="scss">
    .select{
        margin: 10px;
        flex-shrink: 0;
        
        select{
            padding: 5px 10px;
            margin-left: 15px;
        }
    }
</style>