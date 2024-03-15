<template>
  <div>
    <header>
      <h1>The <strong>Movie</strong> Database</h1>
      <form action="" class="search-box" v-on:submit.prevent="handleSearch">
        <input 
        type="search" 
        placeholder="search for a movie..."
        v-model.lazy="search_query"
        required
        >
      </form>
    </header>
    <main>
      <div class="cards" v-if="movieList.length > 0">
        <!-- {{ movieList[0].title }}<br>
        {{ movieList[0].overview }} -->
        <Card v-for="movie in movieList" v-bind:aa="movie"/>
        <!-- aa라는 이름으로 movie가 전달됨 -->
      </div>
      <div class="no-result" v-else>
        <h3>No search results for '{{ search_query }}'</h3>
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Card from './components/Card.vue';
const movieList = ref([])
const search_query = ref('');

const handleSearch = async () => {
  movieList.value = await fetch(`https://api.themoviedb.org/3/search/movie?query=${search_query.value}&include_adult=false&language=en-US&page=1&api_key=4a8fb4ce4fb2d80422bea0acb7bb57ed`)
    .then(response => response.json())
    .then(response => response.results)
  console.log('받아온 데이터', movieList.value)
}

const popular = async () => {
  movieList.value = await fetch('https://api.themoviedb.org/3/movie/popular?language=en-US&page=1&api_key=4a8fb4ce4fb2d80422bea0acb7bb57ed')
    .then(response => response.json())
    .then(response => response.results)
  console.log('받아온 데이터', movieList.value)
}
popular();


</script>

<style lang="scss" scoped>
$color: #313131;
$color2: #638889;

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: sans-serif;
}

header {
  padding: 50px 0;

  h1 {
    color: #638889;
    font-size: 42px;
    font-weight: 400;
    text-align: center;
    margin-bottom: 30px;
    text-transform: uppercase;

    strong {
      color:#2c4748;
    }
  }

  .search-box {
    display: flex;
    justify-content: center;

    input {
      appearance: none;
      border: none;
      outline: none;
      background: #f3f3f3;
      padding: 15px;
      width: 100%;
      max-width: 600px;
      border-radius: 8px;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
      color: $color;
      transition: 0.3s ease-in;

      &::placeholder {
        color: #aaa;

      }

      &:focus {
        background: $color2;
        color: #fff;
      }
    }
  }
}

main {
  margin: auto;
  .cards{
    display: flex;
    flex-wrap: wrap;
    max-width: 1400px;
    margin:auto;
  }
}

.no-result  {
  text-align: center;
}
h3 {color:#fff;}
</style>