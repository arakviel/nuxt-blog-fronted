<script setup>
const runtimeConfig = useRuntimeConfig()

const api = runtimeConfig.public.API_ENDPOINT;

const posts = ref([]);
const currentPage = ref(1);
const lastPage = ref(1);

const fetchPosts = async () => {

  const result = await $fetch(`${api}/posts?page=${currentPage.value}`);
  posts.value = result.data;
  lastPage.value = result.lastPage;
};

const loadPosts = (page) => {
  currentPage.value = page;
  fetchPosts();
};

fetchPosts()
</script>

<template>
  <div>
    <PostList :posts="posts" />
    <Pagination :currentPage="currentPage" :lastPage="lastPage" @onPageChange="loadPosts" />
  </div>
</template>
