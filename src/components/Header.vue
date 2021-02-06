<template>
  <div class="header basePadding">
     <router-link to="/"  >
    <div class="header__logo">MovieLib</div>
     </router-link>
  </div>
</template>

<script>
export default {
  name: 'Header',

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.header
{
  z-index: 100;
  position: absolute;
  top:0px;
  left:0px;
  width:100vw;
  height:100px;
  display: flex;
  justify-content: space-between;
  padding-top:25px;
}
.header__logo
{
  font-size: 3em;
}
.header__search
{
  input 
  {
    border:none;
    background:none;
    font-size: 1.5em;
    border-bottom:solid 1px white;
  }
  img 
  {
    width:50px;
    height:auto;
  }
}
</style>
