<template>
  <div class="app">
    <h1>Document Library</h1>
    <div class="filters">
      <input
        v-model="searchQuery"
        placeholder="Search documents..."
        class="search"
      />
      <select v-model="selectedCategory" class="category">
        <option value="">All Categories</option>
        <option v-for="cat in categories" :key="cat" :value="cat">
          {{ cat }}
        </option>
      </select>
    </div>
    <div v-if="isLoading" class="loading">Loading documents...</div>
    <DocumentList v-else :items="filteredDocuments" />
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
import DocumentList from './components/DocumentList.vue';

const searchQuery = ref('');
const selectedCategory = ref('');
const isLoading = ref(true);
const documents = ref([]);

const mockFetch = () => {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve([
        {
          id: 1,
          title: 'Safety Policy 2024',
          category: 'HR',
          modified: '2024-03-01',
        },
        {
          id: 2,
          title: 'Product Spec Sheet',
          category: 'Engineering',
          modified: '2024-02-15',
        },
        {
          id: 3,
          title: 'Q1 Sales Report',
          category: 'Finance',
          modified: '2024-01-30',
        },
        {
          id: 4,
          title: 'Supplier Contract',
          category: 'Procurement',
          modified: '2024-03-10',
        },
        {
          id: 5,
          title: 'Employee Handbook',
          category: 'HR',
          modified: '2024-03-15',
        },
        {
          id: 6,
          title: 'Leave Policy',
          category: 'HR',
          modified: '2024-02-28',
        },
        {
          id: 7,
          title: 'Budget Forecast FY25',
          category: 'Finance',
          modified: '2024-03-20',
        },
        {
          id: 8,
          title: 'Invoice Template',
          category: 'Finance',
          modified: '2024-01-10',
        },
        {
          id: 9,
          title: 'Circuit Board Spec',
          category: 'Engineering',
          modified: '2024-03-05',
        },
        {
          id: 10,
          title: 'Testing Standards',
          category: 'Engineering',
          modified: '2024-02-20',
        },
        {
          id: 11,
          title: 'Vendor Agreement',
          category: 'Procurement',
          modified: '2024-03-12',
        },
        {
          id: 12,
          title: 'Purchase Order Policy',
          category: 'Procurement',
          modified: '2024-02-05',
        },
      ]);
    }, 2000);
  });
};

onMounted(async () => {
  documents.value = await mockFetch();
  isLoading.value = false;
});

const categories = computed(() => {
  return [...new Set(documents.value.map((doc) => doc.category))];
});

const filteredDocuments = computed(() => {
  return documents.value.filter((doc) => {
    const matchesSearch = doc.title
      .toLowerCase()
      .includes(searchQuery.value.toLowerCase());
    const matchesCategory =
      !selectedCategory.value || doc.category === selectedCategory.value;
    return matchesSearch && matchesCategory;
  });
});
</script>

<style>
.app {
  font-family: sans-serif;
  max-width: 800px;
  margin: 40px auto;
  padding: 0 20px;
}
.filters {
  display: flex;
  gap: 12px;
  margin-bottom: 16px;
}
.search {
  flex: 1;
  padding: 8px 12px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 14px;
}
.category {
  padding: 8px 12px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 14px;
  background: white;
}
.loading {
  text-align: center;
  padding: 40px;
  color: #888;
}
</style>
