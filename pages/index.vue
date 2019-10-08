<template>
  <div id="home-page" class="page-wrapper home-page">
    <site-hero :title="title" :subtitle="subtitle" :image="featureImage">
    </site-hero>
    <main-section theme="one-column">
      <template v-slot:default>
      
      <div class="content">
          <p>
            <strong>Liam Quinn</strong><span> studied & graduated Computer Science, and has subsequently spent the following 8 years working within Digital - particularly around retail.</span> <br><br>
            My experience to date has involved creating mobile apps for retail, planning and development of complex eCommerce solutions for international brands, consulting on replatforming or integrating into an existing system. Having previous experience working with several different eCommerce platforms, I now focus solely on Shopify.        
          </p>
          <br>
        </div>
        
        <!-- All Posts -->
        <posts-grid />
      </template>
      <template v-slot:sidebar>
        Nothing here
      </template>
    </main-section>
    <news-letter-form-modal />
  </div>
</template>

<script>
import { mapState } from 'vuex'
import { setPageData } from '../helper'
import NewsLetterFormModal from '~/components/NewsLetterFormModal'

export default {
  name: 'HomePage',
  head() {
    return {
      title: `Home | ${this.$siteConfig.siteName}`
    }
  },
  components: {
    NewsLetterFormModal
  },
  computed: {
    ...mapState(['title', 'subtitle', 'featureImage'])
  },
  fetch({ store, params }) {
    setPageData(store, { slug: 'home' })
  }
}
</script>

<style>
.home-page .under-subtitle {
  border-top: none;
}
</style>
