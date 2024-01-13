<script setup>
import { ref, computed, onMounted } from "vue";

import BlogPost from "./components/BlogPost.vue";
import PaginatePost from "./components/paginatePost.vue";
import loadingSpinner from "./components/loadingSpinner.vue";

const posts = ref([]);
const postXPage = 10;

const inicio = ref(0);
const fin = ref(postXPage);
const loading = ref(true
);

const Favorito = ref("");

const cambiarFavoritoNombre = (title) => {
  Favorito.value = title; 
};

const next = () => {
  inicio.value = inicio.value + postXPage;
  fin.value = fin.value + postXPage;
};

const previus = () => {
  inicio.value = inicio.value - postXPage;
  fin.value = fin.value - postXPage;
};

const maxLength = computed(() => posts.value.length);

/* onMounted(async () => {
  loading.value = true;
  try {
  const res =  await fetch("https://jsonplaceholder.typicode.com/posts");
  posts.value = await res.json()
  } catch (error) {
    console.log(error);
  } finally{
    setTimeout(() => {
      loading.value = false;
    }, 2000);
  }
}); */

fetch("https://jsonplaceholder.typicode.com/posts")
  .then((res) => res.json())
  .then((data) => (posts.value = data))
  .catch((e)=> console.log(e))
  .finally(() => {
    setTimeout(() => {
      loading.value = false;
    }, 2000);
  });
</script>

<template>
  <loadingSpinner v-if="loading" />

  <div class="container" v-else>
    <h1>App</h1>
    <h2>Mis Post Favoritos: {{ Favorito }}</h2>

    <PaginatePost
      @next="next"
      @prev="previus"
      :inicio="inicio"
      :fin="fin"
      :maxLength="maxLength"
      class="mb-2"
    />

    <BlogPost
      v-for="post in posts.slice(inicio, fin)"
      :key="post.id"
      class="mb-2"
      :title="post.title"
      :id="post.id"
      :body="post.body"
      cambiarFavoritoNombre="cambiarFavoritoNombre"
    >
    </BlogPost>
  </div>
</template>

<style></style>
