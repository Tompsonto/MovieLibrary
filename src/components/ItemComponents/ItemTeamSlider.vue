<template>
  <div class="sliderWrapper sliderPadding" :key="this.$route.params.id">
    <div class="sliderWrapper__header">
      <div class="header__title">{{title}}</div>
      <div class="header__tabsWrapper">
        <span class="header__tabsWrapper_tab--1"><a v-on:click="activeTab='cast'" v-bind:class="[ activeTab === 'cast' ? 'active' : '' ]">Cast</a></span>
        <span class="header__tabsWrapper_tab--2"><a v-on:click="activeTab='crew'" v-bind:class="[ activeTab === 'crew' ? 'active' : '' ]">Crew</a></span>
      </div>
    </div>
      <Carousel :perPage="4" :paginationEnabled="false"  :loop="true"   :navigationEnabled="false"    v-show="activeTab ==='cast'">
      <Slide  v-for="(cast, i) in feed.cast" :key="i"
       :data-index="cast.id"
      @slideclick="handleSlideClickPerson">
      
          <Item :feed="cast"/>
     
      </Slide>
    </Carousel>
    <Carousel :perPage="4" :paginationEnabled="false"  :loop="true"   :navigationEnabled="false"    v-show="activeTab ==='crew'">
      <Slide v-for="(crew, i) in feed.crew" :key="i"
          
          :data-index="crew.id"
          @slideclick="handleSlideClickPerson" >
          <Item  :feed="crew"/>
          
      </Slide>
    </Carousel>

  </div>
</template>

<script>
import { Carousel, Slide } from 'vue-carousel';
export default {
  props:['type'],
  components:{
      Item: () => import("../Item"),
       Carousel,
       Slide
  },
  data(){
    return{
      feed:null,
      page:this.$route.params.id,
      activeTab: 'cast',
    }
  },
  mounted(){
      window.scrollTo(0, 0)
      if (this.type === 'movie')
      {
        this.axios.get('https://api.themoviedb.org/3/movie/'+this.page+'/credits?api_key='+process.env.VUE_APP_API_KEY)
        .then(response => {
        this.feed = response.data;
      })
      }
      else
      {
        this.axios.get('https://api.themoviedb.org/3/tv/'+this.page+'/credits?api_key='+process.env.VUE_APP_API_KEY)
        .then(response => {
        this.feed = response.data;
        })
      }
  },
  methods:{
      handleSlideClickPerson (dataset)  {
      this.$router.push(({ path: `/person/${dataset.index}` }))
    },

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.sliderPadding{
  padding-left:15px;
  padding-right:15px;
}
.sliderWrapper
{
  padding-top: 100px;
}
.header__title
{
  font-size: 4em;
}
.header__tabsWrapper
{
  font-size: 2em;
  padding:25px 0px;
}

a{
   cursor: pointer;
}
  a.active {
   
    color: #484848;
    border-bottom: 2px solid rgb(181, 3, 3);
    cursor: pointer;
}
.header__tabsWrapper_tab--2
{
  padding-left: 25px;
}
</style>
