<template>
  <div class="home">
    <HeroSlider/>
    <Slider/>
    <Slider/>
     <Slider/>
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
