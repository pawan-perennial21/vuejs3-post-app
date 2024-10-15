<template>
  <div>
    <h1>Post Details</h1>
    <div class="post-card" v-if="singlePost">
      <h3>{{ singlePost.title }}</h3>
      <p>{{ singlePost.body }}</p>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';
export default {
  setup() {
    const route = useRoute();
    const singlePost = ref(null);
    onMounted(() => {
      const postId = route.params.id;
      fetch(`https://jsonplaceholder.typicode.com/posts/${postId}`)
        .then((response) => response.json())
        .then((data) => {
          singlePost.value = data;
        });
    });
    return {
      singlePost,
    };
  },
};
</script>

<style scoped>
.read-the-docs {
  color: #888;
}
.post-card {
  padding: 2rem;
  border-radius: 8px;
  background: teal;
  text-align: center;
  width: 100%;
}
</style>
