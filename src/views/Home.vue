<template>
  <div class="home">
    <HeroSlider/>
    <Slider  title="Popular" types="popular"/>
    <Slider  title="Upcoming" types="upcoming"/>
     <Slider title="Top Rated" types="top_rated"/>
  </div>
</template>

<script>



export default {
  name: 'Home',
  components: {
    HeroSlider: () => import("../components/HeroSlider"),
    Slider: () => import("../components/Slider")
  }
}
</script>

<style lang="scss">



</style>
