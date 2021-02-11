<template>
  <div class="itemContentWrapper" :key="this.$route.params.id">
    <div class="itemBackground" v-bind:style="{ 'background-image': 'url(https://image.tmdb.org/t/p/w1920_and_h800_multi_faces/' + feed.backdrop_path + ')' }"></div>
    <div class="itemBackground--overlay"></div>
    <div class="itemContent ">
         <img  v-if="feed.poster_path != null"  :src="'https://image.tmdb.org/t/p/w1280/'+ feed.poster_path">
         <img v-else :src="'https://image.tmdb.org/t/p/w1280/'+ feed.profile_path">
      <div class="itemContent__texts">
        <div v-if="feed.title != null"  class="textsTitle">{{feed.title}}</div>
        <div  v-else class="textsTitle">{{feed.name}}</div>
        <div>

          <div  v-if="feed.release_date != null" class="textsDate">{{feed.release_date}}</div>
          <div v-else class="textsDate">{{feed.birthday}}</div>

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
        <div  v-if="feed.overview != null" class="fullDesc">
         {{feed.overview}}
        </div>
         <div  v-else class="fullDesc">
         {{feed.biography}}
        </div>
        <button  v-if="feed.overview != null" class="btn trailer-btn">Watch Trailer</button>
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
       feed:null
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.itemContentWrapper
{
  position: relative;
  width:100vw;
  min-height: 100vh;
  height:auto;
  display: flex;
  justify-content: center;
  align-items: center;
}

.itemBackground
{
 
  top:0px;
  width:100vw;
  height: 100vh;
  background-position: center;
  filter: blur(10px);
  position: fixed;
}
.itemBackground--overlay
{
  position: fixed;
  z-index: 90;
  width:100vw;
  
  height:100vh;
  top:0px;
  left:0px;
  background:rgba(0,0,0,.3)
}

.itemContent
{
  position: relative;
  top:100px;
  z-index: 99;

  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  img 
  { 
    height:auto;
    width: 60vw;
    border-radius: 10px;
    box-shadow: 2px 2px 19px 2px rgba(0,0,0,0.56);
  } 
}

.itemContent__texts
{
  padding: 0px 15px; 
  display: flex;
  flex-direction: column;
  .textsTitle
  {
    font-size: 2.6em;
    color:white;
    font-weight: bold;
    padding:5px 10px;
  }
  .textsDate
  {
    font-size: 1.7em;
    font-weight: 200;
    padding:0px 10px;
  }
  .textsDetails
  {
    display: flex;
    padding:10px 10px;
   
    .detailsCategory
    {
      font-weight: bold;
    }
  }
  .rate
  {
    padding-top:5px;
    .rateStar
    {
      font-size: 2.2em;
    }
    i 
    {
      color:gold;
    }
  }
  .fullDesc
  {
    position: relative;
    padding:5px;
    max-height: 70vh;
    font-size: 1.1em;
    text-align: justify;
    line-height: 1.45em;
    
  }
}

.trailer-btn
{
  margin-top:10px;
  background:rgb(181, 3, 3);
  color:white;
  font-size:1em;
  width:180px;
}

@media (min-width: 780px) {
  .itemContent{
    padding:0px 15px;
    img
    {
      width:50vw;
    }
    .itemContent__texts
      {
        padding-top: 10px;
        
      }
  }
}

@media (min-width: 1000px){
  .itemContent{
    flex-direction: row;
    width:85vw;
    align-items: flex-start;
    img
    {
      width: 30vw;
      max-width: 450px;
    }
    .fullDesc
    {
      max-width: 45vw;
      overflow-y: auto;
    }

  }
}


</style>
