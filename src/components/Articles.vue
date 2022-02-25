<script setup lang="ts">
import axios from 'axios';
import Article from './Article.vue'
import DocumentationIcon from './icons/IconDocumentation.vue'

</script>

<template>
  <div class="container-fluid">
    <div class="text-center align-middle mt-5 mb-5">
      <div class="spinner-grow" role="status" v-if="loading">
        <span class="visually-hidden">Loading...</span>
      </div>
    </div>

    <Article v-for="article in articles" v-bind:key="article.id">
      <template #image>
        <img v-bind:src="article.id">
      </template>
      <template #heading><h3>{{ article.title }}</h3></template>
      <template #body><p>{{ article.body }}</p></template>

      <div class="clearfix"></div>
      <div class="text-end">
        <a v-bind:href="'/article/'+article.id">Read more</a>
      </div>
    </Article>
  </div>
</template>


<script lang="ts">
export default {
  data() {
    return {
      loading: true,
      articles: [],
    };
  },

  created() {
    this.getData();
  },

  methods: {
    async getData() {
      try {
        const response = await axios.get(
          "http://jsonplaceholder.typicode.com/posts"
        );
        // JSON responses are automatically parsed.
        this.articles = response.data;
      } catch (error) {
        console.log(error);
      }
    },
  }
};
</script>

<style scoped>
</style>
