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
          <a href="/categories/technical-performance" class="panel-block">
            Technical Performance
          </a>
          <a href="/categories/shopify-plus" class="panel-block">
            Shopify Plus
          </a>
          <a href="/categories/ecommerce-strategy" class="panel-block">
            Ecommerce Strategy
          </a>
        </div>
      </template>
  </div>
</template>
