<template>
  <div class="card">
      <img :src="thumb.poster" :alt="thumb.title">
      <h3>{{ thumb.title }}</h3>
      <div class="author">{{ thumb.author }}</div>
      <div class="year">{{ thumb.year }}</div>
      <div class="genre">{{ thumb.genre }}</div>
  </div>
</template>

<script>
export default {
    name: 'Card',
    props: {
        thumb: Object,
    }
}
</script>

<style scoped lang="scss">
    .card{
        text-align: center;
    
        h3{
            margin: 1.4rem 0;
            text-transform: uppercase;
            font-size: 1.3rem;
        }

        .author{
            font-size: 1.15rem;
        }

        .author,
        .year{
            color: #888;
        }
        
        div{
            margin-bottom: .6rem;
        }
    }
</style>