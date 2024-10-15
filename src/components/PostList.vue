<template>
  <div>
    <h1>Post List</h1>
    <div v-if="postList.length">
      <div v-for="post in postList" :key="post.id">
        <router-link class="route-link" :to="/posts/ + post.id"
          >{{ post.id }}) {{ post.title }}</router-link
        >
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
export default {
  setup() {
    const postList = ref([]);

    onMounted(() => {
      fetch('https://jsonplaceholder.typicode.com/posts')
        .then((response) => response.json())
        .then((data) => {
          postList.value = data;
        });
    });
    return {
      postList,
    };
  },
};
</script>

<style scoped>
.read-the-docs {
  color: #888;
}
.route-link {
  margin: 2rem;
  color: white;
  font-size: 1.2rem;
}

.route-link:hover {
  color: teal;
}
</style>
