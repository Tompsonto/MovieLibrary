<template>
  <div class="item-wrapper">
      <ItemContent type="movie"/>
      <ItemTeamSlider type="movie" class="TeamSlider"/>
      <Slider/>
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

.TeamSlider
{
 position: relative;
  top:-250px;
  z-index: 101;
}

</style>
