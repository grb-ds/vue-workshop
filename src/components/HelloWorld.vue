<template>
  <div class="wrapper">
    <!-- Header -->
    <h1 class="header">{{ amount }} Images 📸</h1>

    <!-- Slider -->
    <input class="slider" type="range" min="3" max="60" v-model="amount" />

    <!-- Images -->
    <div class="image__wrapper" v-if="images">
      <a
          class="image__link"
          v-for="image in images"
          :key="image.id"
          :href="image.url"
      >
        <img :src="image.download_url" class="image" />
      </a>
    </div>
  </div>
</template>

<script>
export default {
  created() {
    // This method is executed when page loads
    this.getImages(this.amount);
  },
  data() {
    return {
      amount: 10,
      images: null,
    };
  },
  methods: {
    async getImages(amount) {
      // This method fetches the images
      const response = await fetch(
          `https://picsum.photos/v2/list?limit=${amount}`
      );
      const images = await response.json();
      this.images = images;
    },
  },
  watch: {
    amount() {
      // Everytime the amount changes this code will be executed
      this.getImages(this.amount);
    },
  },
};
</script>

<style scoped>
.wrapper {
  @apply relative container h-full mx-auto px-3 space-y-5;
}

.header {
  @apply mb-4 text-3xl;
}

.slider {
  @apply w-10/12 sm:w-3/6 md:w-72;
}

.image__wrapper {
  @apply grid gap-4 grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-6 items-stretch justify-items-stretch;
}
.image__link {
  @apply w-full;
}
.image {
  @apply object-cover h-52;
  @apply w-full shadow-md rounded-2xl;
  @apply border-2 border-transparent;
  @apply hover:border-gray-800 hover:shadow-xl;
}
</style>

<!--
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      For a guide and recipes on how to configure / customize this project,<br>
      check out the
      <a href="https://cli.vuejs.org" target="_blank" rel="noopener">vue-cli documentation</a>.
    </p>
    <h3>Installed CLI Plugins</h3>
    <ul>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel" target="_blank" rel="noopener">babel</a></li>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-pwa" target="_blank" rel="noopener">pwa</a></li>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-router" target="_blank" rel="noopener">router</a></li>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-vuex" target="_blank" rel="noopener">vuex</a></li>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-eslint" target="_blank" rel="noopener">eslint</a></li>
    </ul>
    <h3>Essential Links</h3>
    <ul>
      <li><a href="https://vuejs.org" target="_blank" rel="noopener">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank" rel="noopener">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank" rel="noopener">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank" rel="noopener">Twitter</a></li>
      <li><a href="https://news.vuejs.org" target="_blank" rel="noopener">News</a></li>
    </ul>
    <h3>Ecosystem</h3>
    <ul>
      <li><a href="https://router.vuejs.org" target="_blank" rel="noopener">vue-router</a></li>
      <li><a href="https://vuex.vuejs.org" target="_blank" rel="noopener">vuex</a></li>
      <li><a href="https://github.com/vuejs/vue-devtools#vue-devtools" target="_blank" rel="noopener">vue-devtools</a></li>
      <li><a href="https://vue-loader.vuejs.org" target="_blank" rel="noopener">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank" rel="noopener">awesome-vue</a></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

&lt;!&ndash; Add "scoped" attribute to limit CSS to this component only &ndash;&gt;
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
-->
