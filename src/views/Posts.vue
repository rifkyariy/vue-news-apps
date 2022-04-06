<template>
  <div class="about grid grid-cols-4">
    <article
      class="px-8 py-3 w-full"
      v-for="item in newsItems"
      v-bind:key="item.id"
    >
      <div class="p-6 rounded-md">
        <img
          class="object-cover object-center w-full h-40 mb-6 rounded"
          v-bind:src="item.newsImage"
          alt="content"
        />

        <h2 class="mb-3 text-lg lg:text-2xl">{{ item.title }}</h2>

        <p class="mb-4 leading-relaxed line-clamp-3">
          {{ item.description }}
        </p>

        <a
          href="#"
          class="
            inline-flex
            items-center
            mt-2
            md:mb-2
            lg:mb-0
            hover:text-blue-400
          "
        >
          Read More
        </a>
      </div>
    </article>
  </div>
</template>

<script>
// eslint-disable-next-line quotes
import axios from "axios";

export default {
  data() {
    return { newsItems: [] };
  },
  async mounted() {
    const url = "https://624bbfb544505084bc5522b0.mockapi.io/news";
    axios
      // eslint-disable-next-line quotes
      .get(url)
      .then((response) => {
        this.newsItems = response.data;
      });
  },
};
</script>
