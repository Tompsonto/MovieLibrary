<template>
  <div class="header basePadding">
    <div class="header__logo">MovieLib</div>
    <div class="header__search">
      <input placeholder="search">
      <img src="https://www.flaticon.com/svg/vstatic/svg/56/56936.svg?token=exp=1611863139~hmac=9443d268abe7b5faf97bdd60ab821d92">
    </div>
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
