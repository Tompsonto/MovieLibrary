<template>
  <div class="item-wrapper">
      <ItemContent  type="person"/>
     
      <Slider/>
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

<style lang="scss">

.TeamSlider
{
 position: relative;
  top:-250px;
  z-index: 101;
}

</style>
