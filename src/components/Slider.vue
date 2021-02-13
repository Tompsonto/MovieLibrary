<template>
  <div class="sliderWrapper">
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
    else if (this.types === 'credits'){
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
      if (this.window.width < 700){
       items = 2
      }
      else if (this.window.width < 820){
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

<style lang="scss" scoped>
 @import '../assets/variables.scss';

.sliderWrapper__header
{
  margin-top:20px;
  padding:10px;
  .header__title 
  {
  color:white;
  font-size: 3em;
  }
  .header__tabsWrapper
  {
    font-size: 1.5em;
    font-family: $second;
    width:150px;
    display: flex;
    justify-content: space-between;
    .active 
    {
      color:$red;
      border-bottom: 2px solid $red;
    }
    span 
    {
      &:hover 
      {
        cursor: pointer;
      }
    }
  }
}

</style>
