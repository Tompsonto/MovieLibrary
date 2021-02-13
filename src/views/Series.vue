<template>
  <div class="item-wrapper">
      <ItemContent  class="content" type="series"/>
      <ItemTeamSlider class="TeamSlider"  types="popular" />
      <Slider class="slider" title="Related" types="related"/>
  </div>
</template>

<script>


import ItemContent from '../components/ItemComponents/ItemContent'
import ItemTeamSlider from '../components/ItemComponents/ItemTeamSlider'
import Slider from '../components/Slider'
export default {
  name: 'Series',
  components: {
    ItemContent,
    ItemTeamSlider,
    Slider
  }
}
</script>

<style lang="scss">


</style>
