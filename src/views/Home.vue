<template>
  <div class="home">
    <HeroSlider/>
    <SliderNew  title="Popular" category="popular"/>
    <SliderNew  title="Upcoming" category="upcoming"/>
    <SliderNew  title="Top Rated" category="top_rated"/>
  </div>
</template>

<script>



export default {
  name: 'Home',
  components: {
    HeroSlider: () => import("../components/HeroSlider"),
    
    SliderNew: () => import("../components/SliderNew")
  },

}
</script>

<style lang="scss">


</style>
