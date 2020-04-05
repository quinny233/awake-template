<template>
  <div id="categories-page" class="page-wrapper categories-page">
    <site-hero title="Categories" image="https://picsum.photos/1800/1801" />
    <main-section theme="sidebar-right">
      <categories-grid />
    </main-section>
    <template v-slot:sidebar>
        <h3 class="subtitle">
          All Categories
        </h3>
        <div class="panel">
          <nuxt-link
            v-for="cat in allCats"
            :key="cat.slug"
            :to="`/categories/${cat.slug}`"
            :class="{
              'panel-block': true,
              'is-active': cat.slug === $route.params.single
            }"
          >
            {{ cat.name }}
          </nuxt-link>
        </div>
      </template>
  </div>
</template>

<script>
export default {
  data() {
    return {
      allCats: []
    }
  },
  async created() {
    this.allCats = await this.$cms.category.getAll()
  }
}
</script>
