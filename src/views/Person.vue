<template>
  <div class="item-wrapper">
      <ItemContent class="content" type="person"/>
      <SliderNew  title="Known from"  class="TeamSlider" category="personCredits"/>
   
  </div>
</template>

<script>


import ItemContent from '../components/ItemComponents/ItemContent'
import SliderNew from '../components/SliderNew'


export default {
  name: 'Person',
  components: {
    ItemContent,
    SliderNew
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
