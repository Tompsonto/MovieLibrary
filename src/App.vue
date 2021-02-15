<template>
  <div id="app">
    <Spinner/>
    <Header class="header"/>

    <div class="mainContent">
   
        <router-view :key="$route.fullPath"/>
   
    </div>
    <Footer class="footer" />
  </div>
</template>



<script>
import Header from './components/Header'
import Footer from './components/Footer'
import Spinner from './components/Spinner'
export default {
  name: 'App',

  components:{
    Header,
    Footer,
    Spinner
  }
}
</script>

<style lang="scss">
  @import './assets/variables.scss';
    *{box-sizing: border-box;}
      html,body{
        padding:0px;
        margin:0px;
        background-color:$black;
      }
#app{
  background:$black;
  font-family: $main;
  max-width: 100%;
}

a, a:visited, a:focus, a:active
{
  text-decoration: none;
  color:white;
}
button 
{
  border:none;
  border-radius: 25px;
  font-family:$second;
  padding:5px 10px;
  &:active, &:visited, &:focus 
  {
    outline: none;
  }
}

.red_btn 
{
  color:white;
  background:$red;
  box-shadow: 0 5px 15px rgba(189, 11, 11, .5);
}

.header, .footer 
{
  position: relative;
  z-index: 102;
}


.mainContent
{
  position: relative;
  z-index: 94;
  min-height: 100vh;
}
</style>
