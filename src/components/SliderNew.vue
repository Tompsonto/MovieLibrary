<template>
  <div class="sliderWrapper">
    <div class="sliderWrapper__header">
      <div class="header__title">{{title}}</div>
      <div class="header__tabsWrapper">
        <span v-show="movies != null" class="header__tabsWrapper_tab--1"><a v-on:click="activeTab='movies'" v-bind:class="[ activeTab === 'movies' ? 'active' : '' ]">Movies</a></span>
        <span v-show="tv != null"  class="header__tabsWrapper_tab--2"><a v-on:click="activeTab='series'" v-bind:class="[ activeTab === 'series' ? 'active' : '' ]">Series</a></span>
        <span v-show="cast != null" class="header__tabsWrapper_tab--1"><a v-on:click="activeTab='cast'" v-bind:class="[ activeTab === 'cast' ? 'active' : '' ]">Cast</a></span>
        <span v-show="crew != null" class="header__tabsWrapper_tab--2"><a v-on:click="activeTab='crew'" v-bind:class="[ activeTab === 'crew' ? 'active' : '' ]">Crew</a></span>
        
      </div>
    </div>
 
    <Carousel :perPage="itemsPerCarousel" :paginationEnabled="false" :navigate-to="4" :navigationEnabled="false"  :loop="true"  v-show="activeTab ==='movies'">
      <Slide v-for="(movie, i) in movies" :key="i"
      :data-index="movie.id"
      @slideclick="handleSlideClickMovie">
     
          <Item :feed="movie"/>
   
      </Slide>
    </Carousel >

    <Carousel  :perPage="itemsPerCarousel" :paginationEnabled="false"  :loop="true"  :navigate-to="4"   :navigationEnabled="false"    v-show="activeTab ==='series'">
      <Slide v-for="(serie, i) in tv" :key="i"  
       :data-index="serie.id"
        @slideclick="handleSlideClickSeries">
       
          <Item :feed="serie"/>
         
      </Slide>
    </Carousel>

    <Carousel :perPage="itemsPerCarousel" :paginationEnabled="false"  :loop="true"  :navigate-to="4"   :navigationEnabled="false"    v-show="activeTab ==='cast'">
      <Slide v-for="(caste, i) in cast" :key="i"  
       :data-index="caste.id"
        @slideclick="handleSlideClickPerson">
       
          <Item :feed="caste"/>
         
      </Slide>
    </Carousel>
    
    <Carousel :perPage="itemsPerCarousel" :paginationEnabled="false"  :loop="true"  :navigate-to="4"   :navigationEnabled="false"    v-show="activeTab ==='crew'">
      <Slide v-for="(crewe, i) in crew" :key="i"  
       :data-index="crewe.id"
        @slideclick="handleSlideClickPerson">
       
          <Item :feed="crewe"/>
         
      </Slide>
    </Carousel>
  </div>
</template>

<script>

const baselink = "https://api.themoviedb.org/3/"
import { Carousel, Slide } from 'vue-carousel';

import Item from './Item'
export default {
  props: ['title','category'],
  components:{
      Item,
       Carousel,
       Slide,
       
  },
  data(){
    return{
      movies:null,
      tv:null,
      cast:null,
      crew:null,
      page:this.$route.params.id,
      activeTab: 'movies',
      window: {
			width: 0,
			height: 0,

      },
    }
  },
  mounted(){
    window.addEventListener("resize", this.handleResize);
    this.handleResize();
    //home sliders
    if (this.category === 'popular'){
       this.axios.get(baselink+'movie/popular?api_key='+process.env.VUE_APP_API_KEY+'&language=en-US&page=1')
        .then(response => {
       this.movies = response.data.results;
        })
        this.axios.get(baselink+'tv/popular?api_key='+process.env.VUE_APP_API_KEY+'&language=en-US&page=1')
        .then(response => {
       this.tv = response.data.results;
        })
    }
    else if (this.category === 'upcoming'){
       this.axios.get(baselink+'movie/upcoming?api_key='+process.env.VUE_APP_API_KEY+'&language=en-US&page=1')
        .then(response => {
       this.movies = response.data.results;
        })
        this.axios.get(baselink+'tv/airing_today?api_key='+process.env.VUE_APP_API_KEY+'&language=en-US&page=1')
        .then(response => {
       this.tv = response.data.results;
        })
    }   
    else if (this.category === 'top_rated'){
       this.axios.get(baselink+'movie/upcoming?api_key='+process.env.VUE_APP_API_KEY+'&language=en-US&page=1')
        .then(response => {
       this.movies = response.data.results;
        }).finally(()=>{this.isLoading = false})
        this.axios.get(baselink+'tv/airing_today?api_key='+process.env.VUE_APP_API_KEY+'&language=en-US&page=1')
        .then(response => {
       this.tv = response.data.results;

        })
    }
    //cast/crew Movie
    else if (this.category === 'castCrewMovie'){
       this.axios.get(baselink+'movie/'+this.page+'/credits?api_key='+process.env.VUE_APP_API_KEY)
       
        .then(response => {
        this.cast = response.data.cast;
       this.crew = response.data.crew;
     
        }).finally(()=>{this.isLoading = false})
        this.activeTab = 'cast'
    }
      //cast/crew Tv
    else if (this.category === 'castCrewTv'){
       this.axios.get(baselink+'tv/'+this.page+'/credits?api_key='+process.env.VUE_APP_API_KEY)
        .then(response => {
       this.cast = response.data.cast;
       this.crew = response.data.crew;
        })
        this.activeTab = 'cast'
    }
    //related movies
     else if (this.category === 'relatedMovies'){
       this.axios.get(baselink+'movie/'+this.page+'/similar?api_key='+process.env.VUE_APP_API_KEY+'&language=en-US&page=1')
        .then(response => {
       this.movies = response.data.results;
        })
        this.activeTab = 'movies'
    }
    //related tv
      else if (this.category === 'relatedTv'){
       this.axios.get(baselink+'tv/'+this.page+'/similar?api_key='+process.env.VUE_APP_API_KEY+'&language=en-US&page=1')
        .then(response => {
       this.tv = response.data.results;
        })
        this.activeTab = 'series'
    }
      //personCredits
      else if (this.category === 'personCredits'){
       this.axios.get(baselink+'person/'+this.page+'/movie_credits?api_key='+process.env.VUE_APP_API_KEY+'&language=en-US&page=1')
        .then(response => {
       this.movies = response.data.cast;
      
        })
      this.axios.get(baselink+'person/'+this.page+'/tv_credits?api_key='+process.env.VUE_APP_API_KEY+'&language=en-US&page=1')
        .then(response => {
       this.tv = response.data.cast;
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
    },
      handleSlideClickPerson (dataset)  {
      this.$router.push(({ path: `/person/${dataset.index}` }))
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
