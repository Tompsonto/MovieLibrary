<template>
  <div class="header basePadding">
     <router-link to="/"  >
    <div class="header__logo">MovieLib</div>
     </router-link>
     <div class="header__search basePadding">
       <input type="text" placeholder="search..." v-model="searchInput"  @keyup.enter="search">
       <button><i class="fas fa-search"></i></button>
       <div class="search__results__wrapper">
         <ul>
           <li v-for="(items, i) in feed" :key="i">
             
            <div v-if="items.media_type == 'movie'">
              <router-link v-bind:to="'/movie/'+items.id" >
               {{items.title}} 
              </router-link>
            </div>
            <div v-else-if="items.media_type == 'person'">
              <router-link v-bind:to="'/person/'+items.id" >
               {{items.name}} 
              </router-link>
            </div>
            <div v-else>
              <router-link v-bind:to="'/person/'+items.id">
               {{items.name}} 
              </router-link>
            </div>
           </li>
         </ul>
       </div>
     </div>
  </div>
</template>

<script>
export default {
  name: 'Header',
  data(){
    return{
      searchToggle: null,
      searchInput:null,
      feed:null,
    }
  },
  methods:{
     search(){
      this.feed = null
      this.axios.get('https://api.themoviedb.org/3/search/multi?api_key='+process.env.VUE_APP_API_KEY+'&language=en-US&query='+this.searchInput+'&include_adult=true')
      .then(response => {
        this.feed = response.data.results;
      })
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
ul, li 
{
  list-style: none;
  padding:0px;
  margin:0px;
  position:relative;
}
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
  button 
  {
    border:none;
    background:none;
    display:none;
    i 
    {
      color:white;
      font-size: 2em;
    }
  }
.header__search
{
  input 
  {
    border:none;
    background:none;
    font-size: 1.5em;
    color:white;
    border-bottom:solid 1px white;
     &::placeholder
  {
    color:white;
  }
  &:active, &:focus 
  {
    caret-color: white;
  }
  
  }
 .search__results__wrapper
 {
   display:none;
   width:300px;
   position: relative;
   z-index:120;
   height:auto;
   padding:5px 10px;
   max-height:75vh;
  background:rgba(0,0,0,.8);
  overflow:auto;
    li 
    {
      position: relative;
      border-bottom: 1px solid gray;
      padding:5px;
      &:hover{
        background:gray;
        cursor: pointer;
      }
    }
 }

}
@media (max-width: 1100px) {
  input
  {
    display:none;
  }
    button 
  {
    border:none;
    background:none;
    display:block;
    i 
    {
      color:white;
      font-size: 2em;
    }
  }

}
 @media (max-width:890px) { 
    .header__logo
    {
     font-size: 1.7em;
    }
 }
</style>
