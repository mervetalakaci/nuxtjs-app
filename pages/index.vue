<template>
  <div class="container">
    <div v-if="error">
      {{ error }}
    </div>
    <ul v-else>
      <li v-for="restaurant in restaurants" :key="restaurant.id">
        {{ restaurant.name }}
      </li>
      <li v-for="category in categories" :key="category.id">
        {{ category.name }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      restaurants: [],
      categories: [],
      error: null
    }
  },
  async mounted () {
    try {
      this.restaurants = await this.$strapi.$restaurants.find()
      this.categories = await this.$strapi.$categories.find()
    } catch (error) {
      this.error = error
    }
  }
}
</script>