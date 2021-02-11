<template>
  <div class="footer basePadding">
    <div class="footer__legal">Created by Tomasz Szymanczak <br>
     with Vue and <a style="text-decoration:underline"  href="https://www.themoviedb.org/" target="_blank">The Movie Database API</a>
     </div>
    <div class="footer__source">
      <a href="https://github.com/Tompsonto" target="_blank">
  <i class="fab fa-github"></i></a>
    </div>

  </div>
</template>

<script>
export default {
  name: 'Footer',

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.footer 
{
  position: relative;
  z-index: 100;
  padding:15px;
  background:black;
  display: flex;
  justify-content: space-between;
      i 
    {
      font-size: 2em;
    }
}
</style>
