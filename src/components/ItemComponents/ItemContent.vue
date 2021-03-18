<template>
  <div class="itemContentWrapper" :key="this.$route.params.id">
    <div v-if="feed.backdrop_path != null " class="itemBackground" v-bind:style="{ 'background-image': 'url(https://image.tmdb.org/t/p/w1920_and_h800_multi_faces/' + feed.backdrop_path + ')' }"></div>
    <div class="itemBackground--overlay"></div>
    <div class="itemContent ">
      <!--Image-->
         <img  v-if="feed.poster_path != null"  :src="'https://image.tmdb.org/t/p/w1280/'+ feed.poster_path">
         <img  v-else :src="'https://image.tmdb.org/t/p/w1280/'+ feed.profile_path">

      <div class="itemContent__texts">
        <!--name/title-->
        <div v-if="feed.title != null"  class="textsTitle">{{feed.title}}</div>
        <div  v-else class="textsTitle">{{feed.name}}</div>
        <div>
        <!--date-->
          <div  v-if="feed.release_date != null" class="textsDate">{{feed.release_date}}</div>
          <div v-else class="textsDate">{{feed.birthday}} <span v-if="feed.deathday != null">- {{feed.deathday}}</span></div>
        <!--movie details-->
          <div class="textsDetails"  v-if="feed.runtime != null">
            <span class="detailsLong">{{feed.runtime}}</span> | 
            <div class="detailsCategory">

              <span class="category" v-for="(cat, i) in feed.genres" :key="i"  >
                {{cat.name}}
              </span>
            </div>
          </div>
          <div  v-if="feed.overview != null" class="rate">
        
            <span class="rateStar"> 
            <i class="fas fa-star"></i>
             {{feed.vote_average}}
            </span>/ 10
          </div>
        </div>
        <!--desc-->
        <div  v-if="feed.overview != null" class="fullDesc">
         {{feed.overview}}
        </div>
         <div  v-else class="fullDesc">
         {{feed.biography}}
        </div>
      </div>
    </div>
   
  </div>
</template>

<script>

export default {
  name: 'ItemContent',
  props: ['type'],
  data(){
    return{
       page:this.$route.params.id,
       feed:null,
       trailer:null,
   
    }
  },

  mounted(){
       window.scrollTo(0, 0)
       if (this.type === 'movie')
       {
          this.axios.get('https://api.themoviedb.org/3/movie/'+this.page+'?api_key='+process.env.VUE_APP_API_KEY+'&language=en-US')
          .then(response => {
          this.feed = response.data;
          })
         
       }
       else if (this.type === 'person')
       {
            this.axios.get('https://api.themoviedb.org/3/person/'+this.page+'?api_key='+process.env.VUE_APP_API_KEY+'&language=en-US')
    .then(response => {
    this.feed = response.data;
    })
       }
       else 
       {
          this.axios.get('https://api.themoviedb.org/3/tv/'+this.page+'?api_key='+process.env.VUE_APP_API_KEY+'&language=en-US')
          .then(response => {
          this.feed = response.data;
          })
       }
  }, 
}
</script>


<style scoped lang="scss">
  @import '../../assets/variables.scss';

  .itemBackground
  {
    position: fixed;
    width:100vw;
    height:100vh;
    max-width: 100%;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover; 
    filter: blur(5px);
  }
  .itemBackground--overlay
  {
    position: fixed;
    width:100vw;
    height:100vh;
    max-width: 100%;
   background:rgba(0,0,0,.3);
   z-index: 90;

  
  }
  .itemContent
  {
   z-index: 94;
    color:white;
    padding:15px;
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    max-width: 100vw;
    width:85vw;
    padding-top: 70px;
    margin: auto;
    img 
    {
      width:100%;
      height:auto;
      border-radius: 15px;
    }
    .itemContent__texts 
    {
      .textsTitle 
      {
        padding-top: 10px;
        font-size:1.8em;
      }
    }
    .textsDetails
    {
      display: flex;
    }
    .rate
    {
      i 
      {
               color:$gold;
          text-shadow: 0px 0px 10px rgba(255,238,0,.8);
      }
    }
    .fullDesc
    {
      padding:10px 0px;
      font-size: 1.2em;
    }
    .btn 
    {
      margin-top:10px;
      font-size: 1.2em;
    }
  }
 @media (min-width: 600px) {
  .itemContent
  {
    z-index: 94;
    color:white;
    padding:15px;
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    max-width: 100vw;
    width:90vw;
    padding-top: 70px;
    margin: auto;
    img 
    {
      width:75%;
      height:auto;
      border-radius: 15px;
    }
  }
 }
  @media (min-width: 800px) {
  .itemContent
  {
    z-index: 94;
    color:white;
    padding:15px;
    position: relative;
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    max-width: 100vw;
    width:90vw;
    padding-top: 70px;
    margin: auto;
    img 
    {
      width:35%;
      height:auto;
      border-radius: 15px;
    }
    .itemContent__texts 
    {
      width:55%;
      padding-left: 15px;
      .textsTitle
      {
        font-size: 3em;
      }
    }
  }
  }
   @media (min-width: 1000px){
    .itemContent
    {
    z-index: 94;
    color:white;
    padding:15px;
    position: relative;
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    max-width: 100vw;
    width:70vw;
    padding-top: 70px;
    margin: auto;
    img 
    {
      width:35%;
      max-width: (95vw/4);
      height:auto;
      border-radius: 15px;
     
    }
    .itemContent__texts 
    {
      width:45%;
      padding-left: 15px;
      font-size: 1.2em;

      .textsTitle
      {
        font-size: 3.4em;
      }
    }
  }
   }
</style>
