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
  width:100vw;
  height:100vh;
  min-height: 800px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.itemBackground
{
  width:100vw;
  height:99vh;
  min-height: 750px;
  background-image: url('https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fimages.wallpapersden.com%2Fimage%2Fdownload%2Ftenet-movie_68298_1920x1080.jpg&f=1&nofb=1');
  background-size: cover;
  background-position: center;
  filter: blur(10px);
  position: sticky;
}
.itemBackground--overlay
{
  position: absolute;
  z-index: 90;
  width:100vw;
  min-height: 750px;
  height:102vh;
  top:0px;
  left:0px;
  background:rgba(0,0,0,.3)
}

.itemContent
{
  
  position: absolute;

  top:20vh;
  z-index: 1000;

  max-width: 1000px;
  min-height: 500px;
  display: flex;
  justify-content: center;
  img 
  { 
    height:56vh;
    min-height:500px;
    border-radius: 10px;
    box-shadow: 2px 2px 19px 2px rgba(0,0,0,0.56);
  } 
}

.itemContent__texts
{
  padding-left: 45px; 
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  .textsTitle
  {
    font-size: 3.3em;
    color:white;
    font-weight: bold;
  }
  .textsDate
  {
    font-size: 1.7em;
    font-weight: 200;
  }
  .textsDetails
  {
    display: flex;
    padding-top:10px;
    .detailsCategory
    {
      font-weight: bold;
    }
  }
  .rate
  {
    padding-top:15px;
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
    padding-top:3vh;
    max-width: 70%;
    font-size: 1.1em;
    text-align: justify;
    line-height: 1.45em;
  }
}

.trailer-btn
{
  margin-top:5vh;
  background:rgb(181, 3, 3);
  color:white;
  font-size:2em;
  width:260px;
}
@media (max-width: 1200px) {
  .itemContentWrapper, .itemBackground, .itemBackground--overlay
  {
    min-height:125vh;
  }
  .itemContent
  {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin: auto;
    width:75vw;
    left:0px;
    right:0px;
    font-size: .8em;

    img 
    {
      height: auto;
      width: 300px;
      min-height: 100px;
    }
    .itemContent__texts
    {
      padding-left: 15px;
      padding-top: 15px;
    }
    .fullDesc
    {
      max-width:90%;
    }
  }
 }
 @media (max-width: 620px){
     .itemContent 
     {
       min-height: 100vh;
       img 
       {
         width:90%;
       }
     }
      .itemContentWrapper, .itemBackground
      {
        position: relative;
        height:145vh;
        min-height: 140vh;
      }
      .itemBackground--overlay
      {
        height:145vh;
          min-height: 140vh;
      }
 }
</style>
