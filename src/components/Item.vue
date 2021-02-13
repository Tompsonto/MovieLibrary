<template>
 <div class="slide">
      <img  v-if="feed.poster_path != null" :src="'https://image.tmdb.org/t/p/w1280/'+ feed.poster_path">
      <img  v-else-if="feed.profile_path != null" :src="'https://image.tmdb.org/t/p/w1280/'+ feed.profile_path">
      <img  v-else class="placeholder" src="../assets/placeholder.png">

    <div v-if="feed.title != null" class="slide__content movie">
      <span class="slide__content__title">{{feed.title}}</span>
      <span class="desc__stars"  v-if="feed.vote_average != null">
        <i class="fas fa-star"></i>{{feed.vote_average}}
      </span>
    </div>

    <div v-if="feed.name != null" class="slide__content series">
      <span v-if="feed.name != null" class="slide__content__name">{{feed.name}}</span>
      <span class="desc__stars"  v-if="feed.vote_average != null">
        <i class="fas fa-star"></i>{{feed.vote_average}}
      </span>
    </div>


    <div v-if="feed.credit_id != null || feed.cast_id != null" class="slide__content person">
      <div  class="character_wrapper">

        <div  class="character_name">{{feed.character}}</div>
        <div  class="character_name">{{feed.job}}</div>

      </div>
    </div>
  </div>
</template>   

<script>
export default {
  name: 'Item',
  props:['feed', 'type']
}
</script>

<style lang="scss" scoped>
  @import '../assets/variables.scss';
  .slide 
  {
    width:calc(93vw/2);
    color:white;
    transition: all ease-in-out .5s;
    
    img 
    {
      width:calc(93vw/2);
      margin:5px;
      box-shadow: 1px 1px 2px 2px rgba(0,0,0,0.75);
      height:auto;
      border-radius: 10px;
      transition: all ease-in-out .5s;
    }
    .slide__content
    {
      width:100%;
      display:flex;
      justify-content: space-between;
      align-items: baseline;
      padding:5px;
      .slide__content__title, .slide__content__name
      {
        font-size: 1.3em;
        width:65%;
        max-height: 75px;
      }
      .desc__stars
      {
        display: flex;
        align-items: center;
        i 
        {
          color:$gold;
          text-shadow: 0px 0px 10px rgba(255,238,0,.8);
          font-size: .9em;
        }
      }
    }
    &:hover 
    {
      transition: all ease-in-out .5s;
      cursor: pointer;
      object-fit: cover;
      overflow: hidden;
      img 
      {
        transition: all ease-in-out .5s;
        transform: scale(.9);
        object-fit: cover;
        overflow: hidden;
       
      }
    }
  }
  @media (min-width: 700px){
  .slide 
  {
    width:calc(93vw/3);
    color:white;
    img 
    {
      width:calc(93vw/3);
      height:auto;
      border-radius: 10px;
    }
  }
  }
   @media (min-width: 820px){
  .slide 
  {
    width:calc(93vw/4);
    color:white;
    img 
    {
      width:calc(93vw/4);
      height:auto;
      border-radius: 10px;
      
    }
      .slide__content
      {
        width:100%;
        display:flex;
        justify-content: space-between;
        align-items: baseline;
        padding:5px;
        .slide__content__title, .slide__content__name
        {
        font-size: 1em;
        width:65%;
        max-height: 75px;
        }
      }
    }
   }
@media (min-width: 1000px){
  .slide 
  {
    width:calc(93vw/5);
    color:white;
    img 
    {
      width:calc(93vw/5);
      height:auto;
      border-radius: 10px;
    }
      .slide__content
      {
        width:100%;
        display:flex;
        justify-content: space-between;
        align-items: baseline;
        padding:5px;
        .slide__content__title, .slide__content__name
        {
        font-size: 1.4em;
        width:65%;
        max-height: 75px;
        }
      }
    }
    }
</style>

