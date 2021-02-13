<template>
  <Carousel  class="heroSlider"  :paginationEnabled="true" :autoplay="false" :loop="true">
    <Slide class="heroSlide" v-for="(movie, i) in feed.slice(0, 8)" :key="i" v-bind:style="{ 'background-image': 'url(https://image.tmdb.org/t/p/w1280/'+ movie.backdrop_path + ')' }">
    <div class="heroOverlay"></div>
    <div class="heroContent">
      <div class="heroStarsWrapper">
        
        <span class="heroStarsWrapper__start">
         <i class="fas fa-star"></i>
          {{movie.vote_average}}
        </span>
         <span class="heroStarsWrapper__date">
          {{movie.release_date}}
        </span>
      </div>
      <div class="heroContent__title">{{movie.title}}</div>

      <div class="heroContent__desc">{{movie.overview|truncate(90)}}</div>
        <router-link v-bind:to="'/movie/'+movie.id"  types="movie">
          <button class="btn red_btn">See more</button>
        </router-link>
    </div>
    </Slide>
  </Carousel>

</template>

<script>
//
import { Carousel, Slide } from 'vue-carousel';
export default {
  name: 'HeroSlider',
  components:{
       Carousel,
       Slide,
  },
  data(){
    return{
        feed:null,
    }
  },
  filters: {
            truncate: function(value) {
                if (value.length > 20) {
                    value = value.substring(0, 200) + '...';
                }
                return value
            }
  },
  mounted(){
      this.axios.get('https://api.themoviedb.org/3/movie/now_playing?api_key='+process.env.VUE_APP_API_KEY+'&language=en-US')
      .then(response => {
        this.feed = response.data.results;
       
      })
  }
}
</script>
<style lang="scss">
 @import '../assets/variables.scss';
.VueCarousel-pagination
{
  position: absolute;
  top:85vh;
  .VueCarousel-dot
  {
    width:calc(75vw/4)!important;
    height:5px!important;
    max-width: 150px;
    border-radius: 0px!important;
    color:$gray!important;
  }
}
</style>

<style scoped lang="scss">
 @import '../assets/variables.scss';
.heroSlider 
{
  width:100vw;
  height:100vh;
  max-width:100%;  
  color:white;
  .heroSlide
  {
    width:100vw;
    height:100vh;
    max-width:100%;  
    background-size: cover ;
    background-repeat: no-repeat ;
    background-position: center;
    .heroOverlay 
    {
      width:100vw;
      height:100vh;
      max-width:100%;  
      background:rgba(0,0,0,.7)
    }
  }
}
  .heroContent 
  {
    position: absolute;
    z-index:95;
    top:70%;
    transform: translateY(-40%);
    width:95vw;
    height:95vh;
    padding:10px;
    .heroStarsWrapper__start 
    {
      font-size: 1.3em;
      i 
      {
        color:$gold;
        text-shadow: 0px 0px 10px rgba(255,238,0,.8);
        
      }
    }
    .heroContent__title
    {
      font-size: 2.5em;
    }
    .heroContent__desc
    {
      font-family: $second;
      width:90%;
      font-size:1.1em;
    }
    button 
    {
      margin-top:10px;
      font-size: 1.4em;
      padding:10px 15px;
    }
  }


@media (min-width: 700px) {
  .heroContent 
  {
    position: absolute;
    z-index:95;
    top:70%;
    transform: translateY(-40%);
    width:95vw;
    height:95vh;
    padding:20px;
    .heroStarsWrapper__start 
    {
      font-size: 1.5em;
      i 
      {
        color:$gold;
        text-shadow: 0px 0px 10px rgba(255,238,0,.8);
        
      }
    }
    .heroContent__title
    {
      font-size: 4em;
    }
    .heroContent__desc
    {
      font-family: $second;
      width:80%;
      font-size:1.2em;
    }
    button 
    {
      margin-top:10px;
      font-size: 1.4em;
      padding:10px 15px;
    }
  }
}
@media (min-width: 1000px){
  .heroContent 
  {
    position: absolute;
    z-index:95;
    top:70%;
    transform: translateY(-40%);
    width:95vw;
    height:95vh;
    padding:10px 45px;
    .heroStarsWrapper__start 
    {
      font-size: 1.3em;
      i 
      {
        color:$gold;
        text-shadow: 0px 0px 10px rgba(255,238,0,.8);
        
      }
    }
    .heroContent__title
    {
      font-size: 5em;
    }
    .heroContent__desc
    {
      font-family: $second;
      width:55%;
      font-size:1.5em;
    }
    button 
    {
      margin-top:10px;
      font-size: 1.4em;
      padding:10px 15px;
    }
  }
}

</style>
