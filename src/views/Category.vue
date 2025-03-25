<template>
  <section>
    <div v-for="(category, index) in filteredCategories" :key="index" class="category-container">
      <div class="category-section">
        <div>
          <h2 class="capitalize-text">{{ category }}</h2>
        </div>
        <div @click="toggleCategory(index)" :class="{ rotated: activeCategories[index] }" class="icon-wrapper">
          <ArrowDown v-if="!activeCategories[index]" />
          <ArrowUp v-else />
        </div>
      </div>
      <div class="items-section" v-if="activeCategories[index]">
        <span v-for="(item, itemIndex) in filteredItems[category]" :key="itemIndex">
          <CardItem :data-item="item" />
        </span>
      </div>
    </div>
  </section>
</template>

<script>
import ArrowDown from '../assets/icon/ArrowDown.vue';
import ArrowUp from '../assets/icon/ArrowUp.vue';
import CardItem from '../components/CardItem.vue';

export default {
  components: {
    ArrowDown,
    ArrowUp,
    CardItem
  },
  props: {
    menuData: {
      type: Object,
      required: true
    },
    searchQuery: {
      type: String,
      default: ''
    },
    selectedCategory: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      activeCategories: {}
    };
  },
  computed: {
    filteredCategories() {
      if (!this.selectedCategory) {
        return this.menuData.menu.map(item => item.category);
      }
      return this.menuData.menu
        .filter(item => item.category === this.selectedCategory)
        .map(item => item.category);
    },
    filteredItems() {
      let filteredData = {};
      this.menuData.menu.forEach((categoryItem) => {
        if (this.selectedCategory && categoryItem.category !== this.selectedCategory) return;

        filteredData[categoryItem.category] = categoryItem.items.filter(item =>
          item.name.toLowerCase().includes(this.searchQuery.toLowerCase())
        );
      });
      return filteredData;
    }
  },
  methods: {
    toggleCategory(index) {
      this.activeCategories[index] = !this.activeCategories[index];
    }
  }
};
</script>
