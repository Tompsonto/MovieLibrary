<template>
  <div class="sliderWrapper " :key="this.$route.params.id">
    <div class="sliderWrapper__header">
      <div class="header__title">{{title}}</div>
      <div class="header__tabsWrapper">
        <span class="header__tabsWrapper_tab--1"><a v-on:click="activeTab='cast'" v-bind:class="[ activeTab === 'cast' ? 'active' : '' ]">Cast</a></span>
        <span class="header__tabsWrapper_tab--2"><a v-on:click="activeTab='crew'" v-bind:class="[ activeTab === 'crew' ? 'active' : '' ]">Crew</a></span>
      </div>
    </div>
      <Carousel :perPage="itemsPerCarousel" :paginationEnabled="false"  :loop="true"   :navigationEnabled="false"    v-show="activeTab ==='cast'">
      <Slide  v-for="(cast, i) in feed.cast" :key="i"
       :data-index="cast.id"
      @slideclick="handleSlideClickPerson">
      
          <Item :feed="cast"/>
     
      </Slide>
    </Carousel>
    <Carousel :perPage="itemsPerCarousel" :paginationEnabled="false"  :loop="true"   :navigationEnabled="false"    v-show="activeTab ==='crew'">
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
      window: {
			width: 0,
			height: 0
      },
    }
  },
  created(){
    window.addEventListener("resize", this.handleResize);
    this.handleResize();
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
  computed:{
       itemsPerCarousel(){
         var items = null
      if (this.window.width < 600){
       items = 2
      }
      else if (this.window.width < 800){
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
  methods:{
    handleResize() {
			this.window.width = window.innerWidth;
			this.window.height = window.innerHeight;
    },
      handleSlideClickPerson (dataset)  {
      this.$router.push(({ path: `/person/${dataset.index}` }))
    },

  },
  destroyed(){
		window.removeEventListener("resize", this.handleResize);
	},
}
</script>


<style scoped lang="scss">
 @import '../../assets/variables.scss';

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
    width:120px;
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
