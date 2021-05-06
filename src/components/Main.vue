<template>
  <main>
      <div v-for="(album, index) in albums" :key="index" class="album">
          <Card :thumb="album" />
      </div>
  </main>
</template>

<script>
import axios from 'axios';

import Card from '@/components/Card.vue'

export default {
    name: 'Main',
    components: {
        Card,
    },
    data(){
        return {
            apiUrl: 'https://flynn.boolean.careers/exercises/api/array/music',
            albums: [],
            loading: true,
        }
    },
    created(){
        this.getAlbums();
    },
    methods: {
        getAlbums(){
            // Call API
            axios.get(this.apiUrl)
            .then(result => {
                this.albums = result.data.response;
            })
            .catch(error => {
                console.log(error);
            });
        }
    },
}
</script>

<style scoped lang="scss">
    main{
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
        padding: 10px 60px;
    }
    .album{
        width: calc(100% / 8 - 34px);
        margin: 20px 17px 0;
        padding: 18px;
        background-color: rgba(#fff, .07);      
    }
</style>