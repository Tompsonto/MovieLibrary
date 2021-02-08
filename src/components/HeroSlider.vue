<template>
  <Carousel class="heroSlider"  :paginationEnabled="true" :autoplay="true" :loop="true">
    
    <Slide class="heroSlide" v-for="(movie, i) in feed.slice(0, 8)" :key="i" v-bind:style="{ 'background-image': 'url(https://image.tmdb.org/t/p/w1280/'+ movie.backdrop_path + ')' }">
    <div class="heroOverlay"></div>
    <div class="heroContent contentPadding">
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

      <div class="heroContent__desc">{{movie.overview|truncate(80)}}</div>
             <router-link v-bind:to="'/movie/'+movie.id"  types="movie">
           <button class="btn btn--main glow-btn">See more</button>
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
       Slide
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style   lang="scss">
.heroSlider
{
.VueCarousel-wrapper
{
  height:100vh;
  .VueCarousel-inner
{
  flex-basis: 100vw!important;
  height:100vh!important
}
}

.VueCarousel-pagination
{
  position: absolute;
  top:90vh;
  .VueCarousel-dot
  {
    border-radius: 0px;
    width:100px!important;
    height:2px!important;
    background:gray!important;
    padding:0px!important;
    margin:0px 15px;
  }
  .VueCarousel-dot--active
  {
    background:red!important
  }
}
}

.heroSlider
{
  width:100vw;
  height:100vh;
  min-height: 600px;
 
 
}
.heroSlide
{
  position: relative;
  width: 100vw;
  
  display: flex;
  align-items: center;
   background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}
.heroOverlay
{
  position: absolute;
  z-index: 90;
  width:100vw;
   min-height: 600px;
  height:100vh;
  top:0px;
  left:0px;
  background:rgba(0,0,0,.8)
}
.heroContent
{
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: flex-start;
  position: relative;
  z-index: 100;
 
  width: 40vw;
  color:white;

}

.heroStarsWrapper
{
  font-size: 1.4em;
  padding-left: 5px;
  padding-bottom: 10px;
  i 
  {
    width:18px;
    height: auto;
    text-shadow: 0 5px 15px rgba(255, 217, 0, 0.35);
    color:gold;
    

  }
}
.heroStarsWrapper__date
{
  padding-left: 25px;
}
.heroContent__title
{
  font-size: 5em;
  text-align: left;
}

.heroMinDesc
{
 display: flex;
 padding-left: 5px;

}
.heroMinDesc__scenario
{
  padding-left: 25px;
}
.heroContent__desc
{
  
  font-size: 1.4em;
  text-align: left;
  padding:20px 0px 0px 5px;
}

.btn--main
{
  background:rgb(181, 3, 3);
  color:white;
  margin:25px 0px 0px 5px;
  font-size: 2em;
  width: 200px;
}

@media (max-width: 1366px) { 
  .heroContent
  {
    width:55vw;
    width:85vw
  }
  .heroContent__desc 
  {
    width:60%;
  }
  
 }
 @media (max-width: 990px) {
   .heroContent{
     font-size: .9em;
   }
  }

 @media (max-width:890px) { 
    .heroContent
    {

      font-size: .9em;
      width:95vw;
    }
   
 }

  @media (max-width:690px) { 
    .heroContent
    {
      top:10vh;
      width: 95vw;
      font-size: .9em;
    }
    .heroContent__desc 
    {
    width:90%;
    }
  
    .VueCarousel-pagination
{
  position: absolute;
  top:87vh;
  .VueCarousel-dot
  {
    border-radius: 0px;
    width:30px!important;
    height:2px!important;
    background:gray!important;
    padding:0px!important;
    margin:0px 15px;
  }
  .VueCarousel-dot--active
  {
    background:red!important
  }
}
 }
</style>
