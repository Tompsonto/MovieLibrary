<template>

  <Carousel  class="heroSlider"  :paginationEnabled="true" :autoplay="false" :loop="true">
    
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style   lang="scss">
.heroWrapper
{
  height:100vh;
  width: 100vw;
}
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
    width:50px!important;
    height:5px!important;
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
  padding:0px 10px;
  width: 85vw;
  color:white;

}

.heroStarsWrapper
{
  font-size: 1.4em;
  padding-left: 5px;
  padding-bottom: 10px;
  display: flex;
  align-items: baseline;
  justify-content: space-between;

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
  font-size: 4em;
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
  
  font-size: 1.3em;
  text-align: left;
  padding:20px 0px 0px 5px;
}

.btn--main
{
  background:rgb(181, 3, 3);
  color:white;
  margin:25px 0px 0px 5px;
  font-size: 1.5em;
  width: 160px;
}


@media (min-width: 780px) {
  .heroContent__desc{
    width:75%;
  }

}

@media (min-width: 1000px) {
  .heroContent
  {
    width:50vw;
    font-size: 1.2em;
    padding:0px 25px;
  }
  .heroContent__desc{
    width:75%;
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
.btn--main
{
  width:200px;
}
}


</style>
