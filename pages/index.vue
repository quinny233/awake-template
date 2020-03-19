<template>
  <div id="home-page" class="page-wrapper home-page">
    <site-hero :title="title" :subtitle="subtitle" :image="featureImage">
    </site-hero>
    <main-section theme="one-column">
      <template v-slot:default>
      
      <div class="column is-offset-2 is-8"> 
        <div class="content">
            <p>
              <span><strong>Liam Quinn</strong> graduated BSc Computer Science at University of Hull, and has subsequently spent the following 8 years working within Digital roles - particularly focused around retail.</span> <br><br>
              My experience to date has involved creation of a mobile app for the retail sector; planning architecture & development of a range of complex eCommerce solutions; consulting on replatforming projects or integrations into existing systems; one-off technical audits, and long term growth strategies. I have experience working with several different eCommerce platforms, with a deep knowledge of Shopify Plus.        
            </p>
            <br>
          </div>
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
.content span{
  font-size:21px;
}
.home-page .under-subtitle {
  border-top: none;
}
</style>
