<template>
  <div class="item-wrapper">
      <ItemContent  class="content" type="movie"/>
     <ItemTeamSlider type="movie" class="TeamSlider" />
     <Slider class="slider" title="Related" types="related"/>
  
  </div>
</template>

<script>


import ItemContent from '../components/ItemComponents/ItemContent'
import ItemTeamSlider from '../components/ItemComponents/ItemTeamSlider'
import Slider from '../components/Slider'
export default {
  name: 'Movie',
  components: {
    ItemContent,
    ItemTeamSlider,
    Slider
  }
}
</script>

<style lang="scss">
.content
{
  position: relative;
}
.TeamSlider,.slider
{
  position: relative;
  z-index: 101;
}

</style>
