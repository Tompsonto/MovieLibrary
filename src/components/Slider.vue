<template>
  <div class="sliderWrapper contentPadding">
    <div class="sliderWrapper__header">
      <div class="header__title">News</div>
      <div class="header__tabsWrapper">
        <span class="header__tabsWrapper_tab--1">Movies</span>
        <span class="header__tabsWrapper_tab--2">Series</span>
      </div>
    </div>
    <Carousel :perPage="5" :paginationEnabled="false"  :navigationEnabled="false">
      <Slide>
          <Item/>
      </Slide>
          <Slide>
          <Item/>
      </Slide>
        <Slide>
          <Item/>
      </Slide>
              <Slide>
          <Item/>
      </Slide>
              <Slide>
          <Item/>
      </Slide>
                <Slide>
          <Item/>
      </Slide>
    </Carousel>
   

  </div>
</template>

<script>
import { Carousel, Slide } from 'vue-carousel';
export default {
  components:{
      Item: () => import("./Item"),
       Carousel,
       Slide
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
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

.header__tabsWrapper_tab--2
{
  padding-left: 25px;
}
</style>
