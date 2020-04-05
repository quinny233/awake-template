<template>
  <footer class="site-footer">
    Liam Quinn &copy; {{ new Date().getFullYear() }}
    <br />
    <a href="/categories">Writing</a> | <a>Twitter</a> | <a>Linkedin</a>
  </footer>
</template>

<script>
export default {
  name: 'SiteFooter'
}
</script>

<style scoped>
footer {
  background: #eee;
  padding: 20px 10px;
  text-align: center;
  transition: 0.5s ease all;
}
</style>
