<template>
  <footer class="footer">
    <div class="footer__legal">Created by Tomasz Szymanczak <br>
     with Vue and <a style="text-decoration:underline"  href="https://www.themoviedb.org/" target="_blank">The Movie Database API</a>
     </div>
    <div class="footer__source">
      <a href="https://github.com/Tompsonto" target="_blank">
  <i class="fab fa-github"></i></a>
    </div>

  </footer>
</template>

<script>
export default {
  name: 'Footer',
}
</script>

<style scoped lang="scss">
.footer 
{
  margin-top: 50px;
  width:100vw;
  max-width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding:10px;
  font-size: 1em;
  color:white;
}
</style>
