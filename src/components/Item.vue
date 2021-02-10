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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">



.slide
{
  width:300px;
  img 
  {
    border-radius: 10px;
    width:300px;
    height: auto;
  }
  .placeholder 
  {
    img 
    {
    border-radius: 10px;
    width:300px;
    height: 500px;
    }
  }

}

.slide__content
{
  width:98%;
  margin: auto;
  display: flex;
  align-items: baseline;
  justify-content: space-between;
}

.slide__content__title, .slide__content__name
{
  font-size: 1.7em;
  text-align: left;
  padding:25px 0px 5px 10px;
  max-width: 75%;
}


.desc__stars
{
  padding-left: 15px;
  
  i 
  {
    padding-right: 10px;
     text-shadow: 0 0px 7px rgba(255, 217, 0, 0.35);
    color:gold;
  }
}

.character_wrapper
{
  display: flex;
  flex-direction: column;
}
</style>
