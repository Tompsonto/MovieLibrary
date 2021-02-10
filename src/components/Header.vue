<template>
  <div class="header">
     <router-link to="/"  >
    <div class="header__logo">MovieLib</div>
     </router-link>
     <div class="header__search ">
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
.header
{
  position: absolute;
  z-index: 150;
  width:99vw;
  display:flex;
  justify-content: space-between;
  padding:15px 10px;
  font-size: 1.7em;
  .header__search
  {
    position: relative;
    input 
    {
     border:none;
    background:none;
    border-bottom:1px solid white;
    display:none;
    }
    button 
    {
      background:none;
      border:none;
      color:white;
      font-size: 1em;
    }
  
  }
}
@media (min-width: 1000px){
  .header 
  {
    padding:25px;
    font-size: 2em;
    .header__search
    {
      display: flex;
      align-items: baseline;
      input 
      {
        display: block;
        width:200px;
      }
    }
  }
}
</style>
