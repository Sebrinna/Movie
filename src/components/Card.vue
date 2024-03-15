<template>
  <div class="card">
    <a :href="`https://www.themoviedb.org/movie/ ${aa.id}`">
      <figure>
        <img v-if="aa.poster_path" :src="`https://media.themoviedb.org/t/p/w300_and_h450_bestv2/${aa.poster_path}`" :alt="aa.title">
        <img v-else src="http://placehold.it/300x400/ddd/333?text=MoviePoster" alt="">
      </figure>

      <div class="text">
        <h3>{{ aa.title }}</h3>
      </div>
    </a>

  </div>
</template>

<script>
export default {
  props: ['aa']
}


</script>

<style lang="scss" scoped>
.card {
  width: 20%;
  padding: 16px;

  @media (max-width:1200px) {
    width: 25%;
  }

  @media (max-width:1024px) {
    width: 33.33%;
  }

  @media (max-width:768px) {
    width: 50%;
  }

  @media (max-width:500px) {
    width: 100%;
  }

  a {
    display: block;
    border-radius: 8px;
    overflow: hidden;
    text-decoration: none;
    color:#111;
    box-shadow: 2px 5px 15px rgba(99, 136, 137, .5);
    

    figure {
      width: 100%;
      height: 0;
      padding-bottom: 150%;
      margin: 0;
      border-radius: 8px;
      overflow: hidden;

      img {
        width: 100%;
        transition: 0.3s ease-in;
      }
    }

    .text {
      height: 80px;
      padding: 16px 16px 0 16px;

      h3 {
        transition: 0.3s ease-in;
      }
    }


    &:hover img {
      transform: scale(1.1);
    }

    &:hover h3 {
      color: #638889;
    }
  }
}
</style>