
<template>
  <div class="nav-wrapper">
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
      <ul>
        <li v-for="(items, i) in feed" :key="i">
         <div  v-if="items.media_type == 'movie'" class="search-item" v-on:click="searchToggle = !searchToggle">
          <router-link v-bind:to="'/movie/'+items.id"  >
            <img v-if="items.poster_path !=null"  class="search-img"  :src="'https://image.tmdb.org/t/p/w1280/'+ items.poster_path"/> 
             <img  v-else class="placeholder" src="../assets/placeholder.png">
             {{items.title}}
          </router-link>
        </div>

        <div  v-else-if="items.media_type == 'tv'" class="search-item" v-on:click="searchToggle = !searchToggle">
          <router-link v-bind:to="'/series/'+items.id"  >
            <img v-if="items.poster_path !=null"  class="search-img"  :src="'https://image.tmdb.org/t/p/w1280/'+ items.poster_path"/> 
           <img  v-else class="placeholder" src="../assets/placeholder.png">
             {{items.name}}
          </router-link>
        </div>

         <div  v-else class="search-item" v-on:click="searchToggle = !searchToggle">
          <router-link v-bind:to="'/person/'+items.id"  >
            <img v-if="items.profile_path !=null"  class="search-img"  :src="'https://image.tmdb.org/t/p/w1280/'+ items.profile_path"/> 
           <img  v-else class="placeholder" src="../assets/placeholder.png">
             {{items.name}}
          </router-link>
        </div>
        </li>
      
      </ul>
    </div>

  </div>
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

ul,li
{
  list-style: none;
  padding:0px;
  margin: 0px;
}
  .nav-wrapper
  {
    z-index: 100;
    position: absolute;
    top:0px;
    left:0px;
    display:flex;
    justify-content: space-between;
    width:99vw;
    padding:15px 10px;
    font-size: 1.5em;
  }

  .overlay
  {
    display:none
  }

  .overlay-active
  {
    display: block;
    position: fixed;
    left:0px;
    top:0px;
    z-index: 200;
    background: rgba(0,0,0,.95);
    width:100vw;
    height:100vh;
    overflow: hidden;
  }

.search-wrapper
{
  input 
  {
    display: none;
  }
}

.search-wrapper
{
 ul 
 {
   display: none;
 }
}

.search-wrapper-active
{
  position: fixed;
  z-index: 201;
  width:100vw;
  margin: auto;
  text-align: center;

  ul 
  {
    margin-top:15px;
   
   display: block;
    text-align: left;
    position: absolute;
    left: 15px;
    max-height: 100vw;
    width:85vw;
    overflow-y: auto;
    li 
    {
      padding-top: 15px;
    }
  }
}

  .search-active
  {

    text-align: center;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    .input-active
    {
      left:0px;
      display:block;
      border:none;
      background: none;
      color:white;
      height: auto;
      border-bottom: 2px solid white;
      width: 85vw;
      font-size: 1.1em;
      padding-bottom: 10px;
      caret-color: red;
      &::placeholder
      {
        color:white;
    
      }
    }
 
  }
    .search-item
    {
      position: relative;
      width:80%;
      padding-top:10px;
      a
      {
        position: relative;
        display: flex;
        align-items: center;
        font-size: .8em;
        word-break: normal;
        img, .placeholder
        {
          position: relative;
          height:130px;
          width: auto;
          padding-right:10px;
        }
      }
    }
  
</style>
