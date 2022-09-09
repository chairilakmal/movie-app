<template>
  <div>
    <div class="py-10 px-20 grid grid-rows-1">
      <div class="grid grid-rows-1 grid-flow-col gap-10 mt-20">
        <div class="row-span-5 ...">
          <p
            class="mb-5 cursor-pointer hover:text-gray-400"
            @click="$router.push('/')"
          >
            Back
          </p>
          <img
            class="rounded-t-lg"
            :src="imageUrl + movies.poster_path"
            style="object-fit: cover; width: 500px; height: 500px"
            alt=""
          />
        </div>
        <div class="col-span-2 mt-10">
          <div>
            <h1 class="text-3xl pb-8 font-bold">{{ movies.title }}</h1>
          </div>
          <div class="text-lg pb-8">
            {{ movies.overview }}
          </div>
          <div class="pb-8 font-bold">
            Rated {{ movies.vote_average }} / by {{ movies.vote_count }} users
          </div>
          <div>
            <button
              class="bg-blue-500 hover:bg-blue-700 text-white py-2 px-4 rounded"
              @click="showAlert"
            >
              <a href="#" class="block py-2 pr-4 pl-3 rounded md:p-0"
                >Give your rating</a
              >
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DetailPage",
  layout: "app",
  data() {
    return {
      movies: [],
      imageUrl: "https://image.tmdb.org/t/p/w600_and_h900_bestv2/",
      apiKey: "bc2ad4500c4db983a0299a03cc13b36a",
      baseUrl: "https://api.themoviedb.org/3/movie/",
    };
  },
  mounted() {
    this.loadMovie();
  },
  methods: {
    loadMovie() {
      this.$axios
        .get(this.baseUrl + this.$route.query.id + "?api_key=" + this.apiKey)
        .then((res) => {
          if (res) {
            this.movies = res.data;
          }
        });
    },
    showAlert: () => {
      alert("Feature under development");
    },
  },
};
</script>

<style scoped></style>
