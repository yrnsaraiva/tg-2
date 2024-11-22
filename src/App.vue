<template>
  <section>
    <div class="container my-5 text-white">
      <Header />
      <div class="row g-4 mt-4" v-if="isLoading">
        <p class="text-center">Loading...</p>
      </div>
      <div class="row g-4 mt-4" v-else-if="error">
        <p class="text-center text-danger">{{ error }}</p>
      </div>
      <div class="row g-4 mt-4" v-else>
        <ResultCard v-for="item in results" :key="item.imdbID" :item="item" />
      </div>
    </div>
  </section>
</template>

<script>
import Header from "./components/Header.vue";
import ResultCard from "./components/ResultCard.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    Header,
    ResultCard,
  },
  data() {
    return {
      apiKey: "apikey 6Kt1sfLrUqNhe4W94HcKMW:7IpNljkbED6o5jnriHRt1r",
      query: "Avengers",
      results: [],
      isLoading: true,
      error: null,
    };
  },
  methods: {
    async fetchIMDBData() {
      const url = `https://api.collectapi.com/imdb/imdbSearchByName?query=${encodeURIComponent(this.query)}`;
      try {
        const response = await axios.get(url, {
          headers: {
            authorization: `apikey ${this.apiKey}`,
            "content-type": "application/json",
          },
        });

        if (response.data.success && response.data.result.length > 0) {
          this.results = response.data.result;
        } else {
          this.error = response.data.message || "No results found";
        }
      } catch (err) {
        this.error = err.message || "Error fetching data";
      } finally {
        this.isLoading = false;
      }
    },
  },
  mounted() {
    this.fetchIMDBData();
  },
};
</script>

<style>
@font-face {
    font-family: 'NetflixSans';
    src: url(/font/NetflixSans-Regular.woff2) format('woff2');
    font-weight: normal;
    font-style: normal;
}
body {
    font-family: 'NetflixSans', sans-serif;
}
.poster-card{
    transition: transform 0.3s ease;
}
.poster-card:hover{
    transform: scale(1.1);
}
</style>
