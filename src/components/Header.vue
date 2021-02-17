
<template>
  <header class="nav-wrapper">
    <div class="logo">
      <router-link to="/">
      MovieLib
      </router-link>
    </div>

    <div class="overlay" :class="{ 'overlay-active': searchToggle }"></div>

    <div class="search-wrapper" :class="{ 'search-wrapper-active': searchToggle }">
      <div class="search" :class="{ 'search-active': searchToggle }">
        <input :class="{ 'input-active': searchToggle }" type="text" placeholder="search..." v-model="searchInput"  @keyup.enter="search" >
     <a v-on:click="searchToggle = !searchToggle"> <i :class="{ 'fas fa-times': searchToggle, 'fas fa-search':!searchToggle  }"></i></a>
     
      </div>
      <ul :class="{ 'list-active': feed }">
        <li v-for="(items, i) in feed" :key="i">
         <div  v-if="items.media_type == 'movie'" class="search-item" v-on:click="searchToggle = !searchToggle">
          <router-link v-bind:to="'/movie/'+items.id"  >
            <img v-if="items.poster_path !=null"  class="search-img"  :src="'https://image.tmdb.org/t/p/w1280/'+ items.poster_path"/> 
             <img  v-else class="placeholder" src="../assets/placeholder.png">
             <p>{{items.title}}</p>
          </router-link>
        </div>

        <div  v-else-if="items.media_type == 'tv'" class="search-item" v-on:click="searchToggle = !searchToggle">
          <router-link v-bind:to="'/series/'+items.id"  >
            <img v-if="items.poster_path !=null"  class="search-img"  :src="'https://image.tmdb.org/t/p/w1280/'+ items.poster_path"/> 
           <img  v-else class="placeholder" src="../assets/placeholder.png">
             <p>{{items.name}}</p>
          </router-link>
        </div>

         <div  v-else class="search-item" v-on:click="searchToggle = !searchToggle">
          <router-link v-bind:to="'/person/'+items.id"  >
            <img v-if="items.profile_path !=null"  class="search-img"  :src="'https://image.tmdb.org/t/p/w1280/'+ items.profile_path"/> 
           <img  v-else class="placeholder" src="../assets/placeholder.png">
            <p> {{items.name}}</p>
          </router-link>
        </div>
        </li>
      
      </ul>
    </div>

  </header>
</template>

<script>


export default {
  name: 'Header',
  data(){
  return{
      searchInput:null,
      searchToggle: false,
      feed:null,  
    }
  },
  watch: {
      searchToggle: function () {
      this.searchInput = null
      this.feed = null
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
      closeAll(){
     
        this.searchInput = null
        this.feed = null
        this.searchToggle = false
      
    }
  },
}
</script>

<style lang="scss" scoped>
.overlay-active 
{
  position: fixed;
  top:0px;
  left: 0px;
  width:100vw;
  max-width: 100%;
  height: 100vh;
  background:rgba(0,0,0,.9);
  z-index: 100;
}
.nav-wrapper 
{
  font-size: 1.6em;
  position: absolute;
  z-index: 90;
  width:100vw;
  max-width: 100%;
  display:flex;
  justify-content: space-between;
  padding:10px 15px;
  z-index: 100;
  input 
  {
    display:none
  }
  i 
  {
    padding:0px;
    margin:0px;
  }
  ul
  {
    list-style: none;
    display: none;
 
  }
  .list-active 
  {
    max-height: 100vh;
    display:block;
    position: absolute;
    left:0px;
    padding:15px;
       overflow: auto;
    li 
    {
      .search-item 
      {
        a
        {
          display: flex;
          align-items: center;
          justify-content: space-between;
        p
        {
          text-align: left;
          width: 100%;
          padding-left: 10px;
        }
        }
      }
      img 
      {
        width:20%;
        height: auto;
      }
    }
  }
}

.search-wrapper-active
{
  position: absolute;
  z-index: 101;
  width:100vw;
  max-width: 100%;
  left:0px;
  top:0px;
}

.search-active 
{
  display: flex;
  width:100vw;
  max-width: 100%;
  justify-content: center;  
  padding-top: 15px;
  input 
  {
    display: block;
    border:none;
    background:none;
    border-bottom: solid 2px white;
    padding:5px;
    width:85%;
    color:white;
    &::placeholder
    {
      color:white;
    }
    &:active,&:active,&:focus
    {
      outline: none;
      caret-color: white;
    }
   
}
}
</style>