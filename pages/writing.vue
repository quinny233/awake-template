<template>
  <div id="writing-page" class="page-wrapper content-page">
    <site-hero
      title="Liam Quinn. Writing Directory"
      subtitle="Just a handy Directory of all the posts I've written in one place. Enjoy!"
      image="/uploads/about-hero.jpg"
    ></site-hero>
    <main-section>
      <template v-slot:default>
        <div class="content">
          <h3>Name of Article</h3>
          <a><p>www.quinny.dev/handleofartice</p></a>
          <small><time datetime="2017-02-14">2017-02-14</time></small>
          <hr>
          <h3>Name of Article</h3>
          <a><p>www.quinny.dev/handleofartice</p></a>
          <small><time datetime="2017-02-14">2017-02-14</time></small>
          <hr> 
        </div>
      </template>

    </main-section>
  </div>
</template>
<style scoped>
h3 {
  margin: 0;
}
</style>
