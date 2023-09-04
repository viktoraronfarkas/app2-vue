<template>
  <div id="app">
    <h1>Comments Data</h1>
    <table class="user-table" v-if="comments.length">
      <thead>
        <tr>
          <th>Post ID</th>
          <th>ID</th>
          <th>Name</th>
          <th>Email</th>
          <th>Body</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="comment in comments" :key="comment.id">
          <td>{{ comment.postId }}</td>
          <td>{{ comment.id }}</td>
          <td>{{ comment.name }}</td>
          <td>{{ comment.email }}</td>
          <td>{{ comment.body }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const start = performance.now();
const comments = ref([]);

const fetchData = async () => {
  const res = await fetch("https://jsonplaceholder.typicode.com/comments");
  const data = await res.json();

  comments.value = data;

  const end = performance.now();
  console.log(`Table loaded in ${end - start} milliseconds`);
};

onMounted(fetchData);
</script>

<style>
.user-table {
  width: 100%;
  border-collapse: collapse;
}

th,
td {
  border: 1px solid black;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #f2f2f2;
}
</style>
