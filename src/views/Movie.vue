<template>

  <div class="item-wrapper">
   
    <ItemContent  class="content" type="movie"/>
 
    <SliderNew  title="Cast/Crew"  class="TeamSlider" category="castCrewMovie"/>
    <SliderNew  title="Related Movies"  class="TeamSlider" category="relatedMovies"/>
    
  
  </div>

</template>

<script>


import ItemContent from '../components/ItemComponents/ItemContent'

import SliderNew from '../components/SliderNew'
export default {
  name: 'Movie',
  components: {
    ItemContent,
    SliderNew
  }
}
</script>

<style scoped lang="scss">
.content 
{
  position: relative;
  z-index:90;
}
.TeamSlider, .slider
{
  position: relative;
  z-index: 91;
}

</style>
