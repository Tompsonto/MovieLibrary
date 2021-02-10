<template>
  <div class="item-wrapper">
      <ItemContent type="series"/>
      <ItemTeamSlider  types="popular" />
      <Slider/>
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
