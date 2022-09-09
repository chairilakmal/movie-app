<template>
  <div>
    <div class="bg-home">
      <div class="mask-group">
        <div class="bg-home-filter"></div>
      </div>
    </div>
    <div class="bg-home-content">
      <div class="grid place-items-center h-screen">
        <div>
          <div class="row flex justify-center mb-8">
            <a href="/" class="flex items-center text-white">
              <img src="../static/main-logo.png" class="mr-3 h-18" alt="" />
              <span
                class="self-center text-xl font-bold whitespace-nowrap text-6xl"
                >Movie App</span
              >
            </a>
          </div>
          <div class="row" style="width: 32rem">
            <form class="flex items-center">
              <label for="search" class="sr-only">Search</label>
              <div class="relative w-full">
                <input
                  class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full pl-2.5 p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                  placeholder="Search your favorite movie.."
                />
              </div>
              <button
                @click="showAlert"
                class="inline-flex items-center py-2.5 px-3 ml-2 text-sm font-medium text-white bg-blue-700 rounded-lg border border-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
              >
                <svg
                  aria-hidden="true"
                  class="mr-2 -ml-1 w-5 h-5"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
                  ></path></svg
                >Search
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>
    <div class="home-content py-10 px-20 grid grid-rows-1">
      <div class="grid lg:grid-cols-4 gap-5 sm:grid-cols-3 mt-14">
        <div v-for="(item, index) in movies" :key="index" class="flex flex-col">
          <div
            class="max-w-sm bg-white rounded-lg border border-gray-200 shadow-md dark:bg-gray-800 dark:border-gray-700 cursor-pointer"
            style="height: 400px"
            @click="$router.push('/detail/?id=' + item.id)"
          >
            <img
              class="rounded-t-lg"
              :src="imageUrl + item.poster_path"
              style="object-fit: cover; width: 300px; height: 225px"
              alt=""
            />
            <div class="p-5">
              <a href="#">
                <h5
                  class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white"
                >
                  {{ item.title }}
                </h5>
              </a>
              <p class="mb-3 font-normal text-gray-700 dark:text-gray-400 pb-2">
                {{ item.release_date }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "IndexPage",
  layout: "app",
  detail: "https://image.tmdb.org/t/p/w600_and_h900_bestv2/",
  data() {
    return {
      movies: [],
      imageUrl: "https://image.tmdb.org/t/p/w600_and_h900_bestv2/",
      apiKey: "bc2ad4500c4db983a0299a03cc13b36a",
      baseUrl: "https://api.themoviedb.org/3/movie/popular",
    };
  },
  async fetch() {
    this.movies = await this.$axios({
      url: this.baseUrl + "?api_key=" + this.apiKey,
      method: "GET",
    }).then((response) => response.data.results);
  },
  fetchOnServer: false,
  methods: {
    showAlert: () => {
      alert("Feature under development");
    },
  },
};
</script>

<style scoped>
.bg-home {
  background-image: url("../static/home-background.jpg");
  height: 100vh;
  background-position: center; /* Center the image */
  background-repeat: no-repeat; /* Do not repeat the image */
  background-size: cover; /* Resize the background image to cover the entire container */
}
.mask-group {
  position: absolute;
  top: 0;
  left: 0 !important;
  bottom: 0;
  right: 0 !important;
}
.bg-home-filter {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  /* White */
  background: #404040;
  opacity: 0.725;
}
.bg-home-content {
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0 !important;
  bottom: 0;
  right: 0 !important;
}
</style>
