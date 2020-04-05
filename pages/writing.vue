<template>
  <div id="about-page" class="page-wrapper about-page content-page">
    <site-hero
      title="Writing Directory"
      subtitle="This is just a handy Directory of all the posts i've written in one place. Enjoy!"
      image="/uploads/about-hero.jpg"
    ></site-hero>
    <main-section>
      <template v-slot:default>
        <div class="content">
          <h3>Name of Article</h3>
          <a>www.quinny.dev/handleofartice</a>
          <time datetime="2017-02-14">2017-02-14</time>
          <hr>
          <h3>Name of Article</h3>
          <a>www.quinny.dev/handleofartice</a>
          <time datetime="2017-02-14">2017-02-14</time> 
        </div>
      </template>

    </main-section>
  </div>
</template>
<script>
import QuoteCard from '~/components/cards/QuoteCard'
export default {
  head() {
    return {
      title: `About | ${this.$siteConfig.siteName}`
    }
  },
  components: { QuoteCard }
}
</script>
