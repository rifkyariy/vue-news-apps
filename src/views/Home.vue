<template>
  <div class="home flex justify-center">
    <div class="w-1/2 px-6">
      <form @submit.prevent="submitForm">
        <div class="mb-6">
          <label
            for="post-title"
            class="
              text-left
              block
              mb-2
              text-sm
              font-medium
              text-gray-900
              dark:text-gray-300
            "
          >
            Post Title
          </label>
          <input
            type="text"
            id="post-title"
            v-model="title"
            class="
              bg-gray-50
              border border-gray-300
              text-gray-900 text-sm
              rounded-lg
              focus:ring-blue-500 focus:border-blue-500
              block
              w-full
              p-2.5
              dark:bg-gray-700
              dark:border-gray-600
              dark:placeholder-gray-400
              dark:text-white
              dark:focus:ring-blue-500
              dark:focus:border-blue-500
            "
            required
          />
        </div>
        <div class="mb-6">
          <label
            for="post-desc"
            class="
              text-left
              block
              mb-2
              text-sm
              font-medium
              text-gray-900
              dark:text-gray-300
            "
            >Image URL</label
          >
          <input
            type="text"
            id="post-desc"
            v-model="imageUrl"
            class="
              bg-gray-50
              border border-gray-300
              text-gray-900 text-sm
              rounded-lg
              focus:ring-blue-500 focus:border-blue-500
              block
              w-full
              p-2.5
              dark:bg-gray-700
              dark:border-gray-600
              dark:placeholder-gray-400
              dark:text-white
              dark:focus:ring-blue-500
              dark:focus:border-blue-500
            "
            required
          />
        </div>
        <div class="mb-6">
          <label
            for="post-author"
            class="
              text-left
              block
              mb-2
              text-sm
              font-medium
              text-gray-900
              dark:text-gray-300
            "
            >Author</label
          >
          <input
            type="text"
            id="post-author"
            v-model="author"
            class="
              bg-gray-50
              border border-gray-300
              text-gray-900 text-sm
              rounded-lg
              focus:ring-blue-500 focus:border-blue-500
              block
              w-full
              p-2.5
              dark:bg-gray-700
              dark:border-gray-600
              dark:placeholder-gray-400
              dark:text-white
              dark:focus:ring-blue-500
              dark:focus:border-blue-500
            "
            required
          />
        </div>
        <div class="mb-6">
          <label
            for="post-title"
            class="
              text-left
              block
              mb-2
              text-sm
              font-medium
              text-gray-900
              dark:text-gray-300
            "
          >
            Description / Paragraph
          </label>
          <textarea
            v-model="description"
            class="
              bg-gray-50
              border border-gray-300
              text-gray-900 text-sm
              rounded-lg
              focus:ring-blue-500 focus:border-blue-500
              block
              w-full
              p-2.5
              dark:bg-gray-700
              dark:border-gray-600
              dark:placeholder-gray-400
              dark:text-white
              dark:focus:ring-blue-500
              dark:focus:border-blue-500
              resize-none
            "
            rows="5"
          ></textarea>
        </div>
        <div class="text-right">
          <button
            type="submit"
            class="
              text-white
              bg-blue-700
              hover:bg-blue-800
              focus:ring-4 focus:outline-none focus:ring-blue-300
              font-medium
              rounded-lg
              text-sm
              w-full
              sm:w-auto
              px-5
              py-2.5
              text-center
              dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800
            "
          >
            Submit
          </button>
        </div>
      </form>
    </div>
    <div class="w-1/4">
      <label
        for="post-preview"
        class="
          text-left
          block
          mb-2
          text-sm
          font-medium
          text-gray-900
          dark:text-gray-300
        "
      >
        Post Preview
      </label>
      <div class="rounded-md shadow-md">
        <img
          class="object-cover object-center w-full h-40 mb-6 rounded"
          v-bind:src="
            imageUrl == '' ? 'http://via.placeholder.com/250x250' : imageUrl
          "
        />
        <div class="px-6 pb-6">
          <h2 class="text-lg lg:text-2xl text-left">
            {{ title == "" ? "Post Title" : title }}
          </h2>
          <div class="flex justify-between">
            <span class="text-xs">
              By
              <a class="hover:text-blue-400" href="/">
                {{ author == "" ? "Author" : author }}</a
              >
            </span>
            <span class="text-xs">
              <i class="fas fa-calendar-alt"></i> {{ createdAt }}
            </span>
          </div>
          <p class="my-4 line-clamp-4 text-left">
            {{
              description == ""
                ? "It is a long established fact that a reader will be distracted by the "
                : description
            }}
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
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Home",
  components: {},
  data() {
    return {
      title: "",
      imageUrl: "",
      description: "",
      author: "",
      createdAt: this.currentDate(),
    };
  },
  methods: {
    currentDate() {
      const today = new Date();
      const date = `${today.getFullYear()}/${
        today.getMonth() + 1
      }/${today.getDate()}`;
      // const time = `${today.getHours()}:${today.getMinutes()} `;
      const dateTime = `${date}`;

      return dateTime;
    },
    submitForm() {
      const url = "https://624bbfb544505084bc5522b0.mockapi.io/news";
      axios
        .post(url, {
          title: this.title,
          createdAt: this.createdAt,
          description: this.description,
          author: this.author,
          newsImage: this.imageUrl,
        })
        .then((response) => console.log(response))
        .catch((error) => console.log(error));
    },
  },
};
</script>
