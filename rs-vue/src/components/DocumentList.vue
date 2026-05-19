<template>
  <table class="list">
    <thead>
      <tr>
        <th>Title</th>
        <th>Category</th>
        <th>Modified</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in items" :key="item.id">
        <td>{{ item.title }}</td>
        <td>{{ item.category }}</td>
        <td>{{ item.modified }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script setup>
defineProps(['items']);
</script>

<style>
.list {
  width: 100%;
  border-collapse: collapse;
}
.list th,
.list td {
  text-align: left;
  padding: 10px 12px;
  border-bottom: 1px solid #ddd;
}
.list th {
  background: #f4f4f4;
  font-weight: 600;
}
.list tr:hover td {
  background: #fafafa;
}
</style>
