<template>
    <main>
        <Select @selection="choose" :genre="albums"/>
        <section v-if="!loading" class="albums-sect">
            <div v-for="(album, index) in filterByGenre" :key="index" class="album">
                <Card :thumb="album" />
            </div>
        </section>
        <Loader v-else />
    </main>
</template>

<script>
import axios from 'axios';

import Card from '@/components/Card.vue'
import Loader from '@/components/Loader.vue'
import Select from '@/components/Select.vue'

export default {
    name: 'Main',
    components: {
        Card,
        Loader,
        Select,
    },
    data(){
        return {
            apiUrl: 'https://flynn.boolean.careers/exercises/api/array/music',
            albums: [],
            loading: true,
            selectedGenre: 'all',
        }
    },
    computed: {
        filterByGenre(){
            if(this.selectedGenre === 'all'){
                return this.albums;
            }
            return this.albums.filter(item => item.genre.toLowerCase() === this.selectedGenre);
        }
    },
    created(){
        this.getAlbums();
    },
    methods: {
        /**
         * Get albums list
         */
        getAlbums(){
            // Call API
            axios.get(this.apiUrl)
            .then(result => {
                this.albums = result.data.response;
                this.loading = false;
            })
            .catch(error => {
                console.log(error);
            });
        },

        choose(option){
            this.selectedGenre = option;
        }
    },
}
</script>

<style scoped lang="scss">
    main{
        padding: 10px 60px;

        .albums-sect{
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
        }
        .album{
            flex-basis: 185px;
            margin: 20px 17px 0;
            padding: 18px;
            background-color: rgba(#fff, .07);      
        }
    }
</style>