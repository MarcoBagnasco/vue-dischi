<template>
    <div class="select flex jc-center">
        <label for="genre">Filter by genre:</label>
        <select name="genre" id="genre" v-model="option" @change="$emit('selection', option)">
            <option value="all">All</option>
            <option v-for="(item, index) in getGenre" :key="index" :value="item.toLowerCase()">{{item}}</option>
        </select>
    </div>
</template>

<script>
export default {
    name: 'Select',
    props: {
        genre: Array,
    },
    data(){
        return {
            option: 'all',
            genreList : [],
        }
    },
    computed: {
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
        margin-bottom: 15px;
        
        select{
            margin-left: 20px;
        }
    }
</style>