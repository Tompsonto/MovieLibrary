<template>
  <div class="item-wrapper">
      <ItemContent class="content" type="person"/>
      <Slider class="slider" title="Known from" types="credits"/>
   
  </div>
</template>

<script>


import ItemContent from '../components/ItemComponents/ItemContent'
import Slider from '../components/Slider'


export default {
  name: 'Person',
  components: {
    ItemContent,
    Slider
  }
}
</script>

<style  lang="scss">
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
