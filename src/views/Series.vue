<template>
  <div class="item-wrapper">
      <ItemContent  class="content" type="series"/>
      <SliderNew  title="Cast/Crew"  class="TeamSlider" category="castCrewTv"/>
    
    <SliderNew  title="Related TV"  class="TeamSlider" category="relatedTv"/>
  </div>
</template>

<script>


import ItemContent from '../components/ItemComponents/ItemContent'

import SliderNew from '../components/SliderNew'
export default {
  name: 'Series',
  components: {
    ItemContent,

    SliderNew
  }
}
</script>

<style lang="scss">


</style>
