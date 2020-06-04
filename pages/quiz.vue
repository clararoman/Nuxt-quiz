<template>
  <div class="category-wrapper">
    <h2>Choose your category</h2>
    <div class="row">
      <div class="col-3" v-for="(category, i) in sortedArray" :key="i">
        <div>
          <nuxt-link :to="'/category/'+category.id">
            <b-button pill size="sm" class="col-12 choose-category">{{category.name}}</b-button>
          </nuxt-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      selectedCategory: ""
    };
  },
  async asyncData({ params }) {
    const categories = await axios.get("https://opentdb.com/api_category.php");
    return {
      categories: categories.data.trivia_categories
    };
  },
  computed: {
    entertainment() {
      let list = [];
      this.categoryNames.forEach(item => {
        if (item.includes("Entertainment")) {
          list.push(item);
        }
      });
      return list;
    },
    sortedArray() {
      function compare(a, b) {
        if (a.name < b.name) return -1;
        if (a.name > b.name) return 1;
        return 0;
      }
      return this.categories.sort(compare);
    },
    categoryNames() {
      let names = [];
      this.categories.forEach(category => {
        names.push(category.name);
      });
      return names;
    }
  }
};
</script>

<style lang="scss">
.category-wrapper {
  position: relative;
  h2 {
    margin: 2rem 0;
    text-align: center;
  }
  button.choose-category {
    padding: 1rem;
  }
}
</style>