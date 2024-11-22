<template>
  <div class="col-md-2 col-10 mb-4 mx-auto">
    <div class="card h-60 rounded-0 border-0 shadow-sm poster-card" style="background:#141414;">
      <a :href="'https://www.imdb.com/title/' + item.imdbID + '/?ref_=fn_al_tt_1'" target="_blank">
        <img :src="item.Poster" class="card-img-top rounded-0 poster" :alt="item.Title">
      </a>
      <div class="card-body text-white">
        <h6 class="card-title">{{ item.Title }}</h6>
        <p class="card-text" style="font-size: 0.780rem">
          {{ item.Year }} {{ item.Type }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ResultCard",
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>

</style>
