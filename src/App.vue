<template>
  <div class="app-container">
    <Header @search="searchQuery = $event" @category-change="selectedCategory = $event" :menu-data="MenuData"/>
    <Category :menu-data="MenuData" :search-query="searchQuery" :selected-category="selectedCategory" />
  </div>
</template>

<script>
import MenuData from './MenuData.json';
import Category from './views/Category.vue';
import Header from './views/Header.vue';

export default {
  name: 'App',
  components: {
    Category,
    Header
  },
  data() {
    return {
      MenuData,
      searchQuery: '', // Store search input value
      selectedCategory: '' // Store selected category
    };
  }
};
</script>
