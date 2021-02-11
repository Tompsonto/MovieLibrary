<template>
  <div class="sliderWrapper sliderPadding">
    <div class="sliderWrapper__header">
      <div class="header__title">{{title}}</div>
      <div class="header__tabsWrapper">
        <span class="header__tabsWrapper_tab--1"><a v-on:click="activeTab='movies'" v-bind:class="[ activeTab === 'movies' ? 'active' : '' ]">Movies</a></span>
        <span class="header__tabsWrapper_tab--2"><a v-on:click="activeTab='series'" v-bind:class="[ activeTab === 'series' ? 'active' : '' ]">Series</a></span>
      </div>
    </div>
    <Carousel :perPage="itemsPerCarousel" :paginationEnabled="false" :navigate-to="4" :navigationEnabled="false"  :loop="true"  v-show="activeTab ==='movies'">
      <Slide v-for="(movie, i) in movies" :key="i"
      :data-index="movie.id"
      @slideclick="handleSlideClickMovie">
     
          <Item :feed="movie"/>
   
      </Slide>
    </Carousel >
       <Carousel :perPage="itemsPerCarousel" :paginationEnabled="false"  :loop="true"  :navigate-to="4"   :navigationEnabled="false"    v-show="activeTab ==='series'">
      <Slide v-for="(serie, i) in series" :key="i"  
       :data-index="serie.id"
        @slideclick="handleSlideClickSeries">
       
          <Item :feed="serie"/>
         

      </Slide>
        
    </Carousel>

  </div>
</template>

<script>


import { Carousel, Slide } from 'vue-carousel';
export default {
  props: ['title', 'types'],
  components:{
      Item: () => import("./Item"),
       Carousel,
       Slide
  },
  data(){
    return{
      movies:null,
      series:null,
      page:this.$route.params.id,
      activeTab: 'movies',
      window: {
			width: 0,
			height: 0
      },
    }
  },

  created(){
    window.addEventListener("resize", this.handleResize);
    this.handleResize();
        if (this.types === 'related'){
         this.axios.get('https://api.themoviedb.org/3/movie/'+this.page+'/similar?api_key='+process.env.VUE_APP_API_KEY+'&language=en-US&page=1')
        .then(response => {
        this.movies = response.data.results;
      })
       this.axios.get('https://api.themoviedb.org/3/tv/'+this.page+'/similar?api_key='+process.env.VUE_APP_API_KEY+'&language=en-US&page=1')
        .then(response => {
        this.series = response.data.results;
      })
    }
    else if (this.type === 'credits'){
        this.axios.get('https://api.themoviedb.org/3/person/'+this.page+'/tv_credits?api_key='+process.env.VUE_APP_API_KEY+'&language=en-US&page=1')
          .then(response => {
        this.movies = response.data.results;
      })
       this.axios.get('https://api.themoviedb.org/3/person/'+this.page+'/movie_credits?api_key='+process.env.VUE_APP_API_KEY)
        .then(response => {
        this.series = response.data.results;
      })
    }
    else{
      this.axios.get('https://api.themoviedb.org/3/movie/'+this.types+'?api_key='+process.env.VUE_APP_API_KEY+'&language=en-US&page=1')
        .then(response => {
        this.movies = response.data.results;
      })
      this.axios.get('https://api.themoviedb.org/3/tv/'+this.types+'?api_key='+process.env.VUE_APP_API_KEY+'&language=en-US&page=1')
        .then(response => {
        this.series = response.data.results;
      })
    }
    if (this.types === 'upcoming'){
        this.axios.get('https://api.themoviedb.org/3/tv/airing_today?api_key='+process.env.VUE_APP_API_KEY+'&language=en-US&page=1')
        .then(response => {
        this.series = response.data.results;
      })
    }
  },

  methods: {
		handleResize() {
			this.window.width = window.innerWidth;
			this.window.height = window.innerHeight;
    },
      handleSlideClickSeries (dataset)  {
      this.$router.push(({ path: `/series/${dataset.index}` }))
    },
      handleSlideClickMovie (dataset)  {
      this.$router.push(({ path: `/movie/${dataset.index}` }))
    }
  },

    computed:{
       itemsPerCarousel(){
         var items = null
      if (this.window.width < 600){
       items = 2
      }
      else if (this.window.width < 800){
        items = 3
      }
      else if (this.window.width < 1000){
        items = 4
      }
      else{
        items = 5
      }
      return items
    }
  },

   destroyed() {
		window.removeEventListener("resize", this.handleResize);
	},

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
.sliderWrapper
{
  .VueCarousel-slide
  {
  padding-left: 10px;
  }
}
</style>

<style scoped lang="scss">

.sliderPadding{
  padding-left:15px;
  padding-right:15px;
}
a, a:active, a:visited
{
  color:white;
  text-decoration: none;
}

.sliderWrapper
{
  padding-top: 100px;
}
.header__title
{
  font-size: 4em;
}
.header__tabsWrapper
{
  font-size: 2em;
  padding:25px 0px;
}

a{
   cursor: pointer;
}
  a.active {
   
    color:rgb(181, 3, 3);
    text-shadow: 0 0px 7px rgba(181,3, 30, 0.35);
    border-bottom: 2px solid rgb(181, 3, 3);
    cursor: pointer;
}
.header__tabsWrapper_tab--2
{
  padding-left: 25px;
}


</style>
