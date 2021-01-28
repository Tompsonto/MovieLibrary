<template>
  <div id="app">
    <Header/>
    <div class="mainContent">
    <router-view/>
    </div>
    <Footer/>
  </div>
</template>



<script>
import Header from './components/Header'
import Footer from './components/Footer'
export default {
  name: 'App',
  components:{
    Header,
    Footer
  }
}
</script>

<style lang="scss">
p{
  margin:0px;
  padding:0px;
}

.basePadding
{
  padding:0px 45px;
}
.contentPadding
{
  padding:0px 100px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color:white;
  background: black;
  height:100vh;
}
.btn
{
  border:none;
  border-radius: 55px;
  padding:10px 15px;
   box-shadow: 0 5px 15px rgba(181, 3, 3, .4);
}


 @media (max-width:890px) { 
    .basePadding
    {
       padding:0px 15px;
    }
 }
</style>
