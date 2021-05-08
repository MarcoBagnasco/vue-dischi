<template>
    <main>
        <div class="filters-wrap flex ai-center">
            <Filters v-if="!loading" >
                <Select @selection="chooseGenre" :genre="albums" :option="selectedGenre"/>
                <Search @AuthorSearch="chooseAuthor" searching="Author"/>
                <Search @TitleSearch="chooseTitle" searching="Title"/>
            </Filters>
            <!-- Filter Messages -->
            <div v-show="selectedAuthor !== ''" class="look-for">Looked for Author : <span>"{{selectedAuthor}}"</span></div>
            <div v-show="selectedTitle !== ''" class="look-for">Looked for Title : <span>"{{selectedTitle}}"</span></div>
            <div v-show="selectedGenre !== 'all'" class="look-for">Looked for Genre : <span>"{{selectedGenre}}"</span></div>
        </div>

        <!-- ALBUMS -->
        <section v-if="!loading" class="albums-sect flex jc-center">
            <div v-for="(album, index) in filterAlbums" :key="index" class="album">
                <Card :thumb="album" />
            </div>
        </section>

        <Loader v-else />
    </main>
</template>

<script>
// AXIOS
import axios from 'axios';

// COMPONENTS
import Card from '@/components/Card.vue'
import Loader from '@/components/Loader.vue'
import Select from '@/components/Select.vue'
import Filters from '@/components/Filters.vue'
import Search from '@/components/Search.vue'

export default {
    name: 'Main',
    components: {
        Card,
        Loader,
        Select,
        Filters,
        Search,
    },
    data(){
        return {
            loading: true,
            apiUrl: 'https://flynn.boolean.careers/exercises/api/array/music',
            albums: [],
            selectedGenre: 'all',
            selectedAuthor: '',
            selectedTitle: '',
        }
    },
    computed: {
        /**
         * Choose array to loop
         */
        filterAlbums(){
            if(this.selectedAuthor !== ''){
                return this.filterByAuthor();
            }
            if(this.selectedTitle !== ''){
                return this.filterByTitle();
            }   
            return this.filterByGenre();
        },

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

        /**
         * Return array filtered by genre
         */
        filterByGenre(){
            if(this.selectedGenre === 'all'){
                return this.albums;
            }
            return this.albums.filter(item => item.genre.toLowerCase() === this.selectedGenre);
        },
        /**
         * Return array filtered by author
         */
        filterByAuthor(){
            if(this.selectedAuthor === ''){
                return this.albums;
            }
            return this.albums.filter(item => item.author.toLowerCase().includes(this.selectedAuthor.toLowerCase()));
        },
        /**
         * Return array filtered by title
         */
        filterByTitle(){
            if(this.selectedTitle === ''){
                return this.albums;
            }
            return this.albums.filter(item => item.title.toLowerCase().includes(this.selectedTitle.toLowerCase()));
        },

        /**
         * Change genre
         */
        chooseGenre(option){
            this.selectedAuthor = '';
            this.selectedTitle = '';
            this.selectedGenre = option;
        },
        /**
         * Change author
         */
        chooseAuthor(author){
            this.selectedTitle = '';
            this.selectedGenre = 'all';
            this.selectedAuthor = author;
        },
        /**
         * Change title
         */
        chooseTitle(title){
            this.selectedAuthor = '';
            this.selectedGenre = 'all';
            this.selectedTitle = title;
        }
    },
}
</script>

<style scoped lang="scss">
// VARIABLES SCSS
@import '@/styles/variables.scss';

    main{
        padding: 10px 60px;

        .look-for{
            margin-left: 30px;
            font-size: 1.3rem;

            span{
                padding: 0 10px;
            }
        }

        .albums-sect{
            flex-wrap: wrap;
        }

        .album{
            flex-basis: 185px;
            margin: 20px 17px 0;
            padding: 18px;
            background-color: $bg-elements;      
        }
    }
</style>