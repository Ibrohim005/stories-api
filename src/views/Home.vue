<template>
  <div class="lg:container mx-auto text-center px-20">
    <h1 class="p-5 text-4xl text-red-500">Top art stories:</h1>
    <div class="cards grid grid-cols-1 lg:grid-cols-2 gap-4">
      <div
        class="card flex flex-col sm:flex-row bg-white rounded-xl"
        v-for="(item, index) in stories.results"
        :key="index"
      >
        <img
          :src="item.multimedia[0].url"
          alt=""
          class="card__img w-100 h-full rounded-xl mx-auto"
        />
        <div class="card-right p-3">
          <h2 class="text-red-500">{{ item.title }}</h2>
          <p class="card__text my-4">{{ item.abstract }}</p>
          <a :href="item.url" class="card__link text-blue-500"
            >More Information...</a
          >
        </div>
      </div>
    </div>
    <div
      class="bg-gray-200 w-full h-screen fixed top-0 left-0"
      style="z-index: -1"
    ></div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Home",
  data() {
    return {
      api_key: "S67jCAts92RSo1WyjFXqDIMm8o0cXMHs",
      url_base: "https://api.nytimes.com/svc/topstories/v2/",
      query: "arts",
      stories: {
        results: [
          {
            abstract:
              "The actress is drawing Oscar talk for her portrayal of Princess Diana in “Spencer,” a role that required the sort of performance she had never given before.",
            title: "Kristen Stewart’s Princess Diaries",
            url: "",
            multimedia: [
              {
                url: "",
              },
            ],
          },
        ],
      },
    };
  },
  created: function () {
    this.fetchStories();
  },
  methods: {
    fetchStories() {
      axios
        .get(`${this.url_base}${this.query}.json?api-key=${this.api_key}`)
        .then((response) => {
          this.stories = response.data;
          console.log(this.stories);
        })
        .catch((e) => {
          console.log(e);
        });
    },
  },
};
</script>

<style lang="scss">
.bg {
  transform: translate(-50%, 0);
  z-index: -1;
}
.main {
  &-info {
    background-color: rgba(255, 255, 255, 0.6);
  }
  &__temp {
    font-size: 80px;
  }
}
.card {
  text-align: left;
  &__img {
    width: 150px;
  }
}
</style>
