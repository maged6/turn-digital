<template>
    <header> 
      <div class="d-flex aline-items-center justify-content-between w-100 flex-wrap">
        <div>
          <h1> Menu </h1>
        </div>
        <div class="d-flex aline-items-center justify-content-end flex-wrap w-80 gap-1">
          <select v-model="selectedCategory" @change="$emit('category-change', selectedCategory)">
            <option value="">All Categories</option>
            <option v-for="(category, index) in categories" :key="index" :value="category">
              {{ category }}
            </option>
          </select>
          <input type="text" placeholder="Search" class="input-text" v-model="searchText" @input="$emit('search', searchText)" />
        </div>
      </div>
    </header>
  </template>
  
  <script>
  export default {
    props: {
      menuData: {
        type: Object,
        required: true
      }
    },
    data() {
      return {
        searchText: '',
        selectedCategory: ''
      };
    },
    computed: {
      categories() {
        return this.menuData.menu.map(item => item.category)
      }
    }
  };
  </script>
  