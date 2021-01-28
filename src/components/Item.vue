<template>
 <div class="slide">
      <img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fimages.wallpapersden.com%2Fimage%2Fdownload%2Ftenet-movie_68298_2764x4096.jpg&f=1&nofb=1">
    <div class="slide__content">
      <span class="slide__content__title">TENET</span>
   
        <span class="desc__stars">
       <img  src="https://www.flaticon.com/svg/vstatic/svg/1828/1828884.svg?token=exp=1611861781~hmac=b095d56eca9d415a1f4ee0573a4959b5">
        8
        </span>
        
    
    </div>
    </div>
</template>   

<script>
export default {
  name: 'Item',

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">



.slide
{
  width:300px;
  img 
  {
    border-radius: 10px;
    width:300px;
    height: auto;
  }
}

.slide__content
{
  width:100%;
  display: flex;
  align-items: baseline;
  justify-content: space-between;
}

.slide__content__title
{
  font-size: 2em;
  text-align: left;
  padding:25px 0px 15px 0px;
}


.desc__stars
{
  padding-right: 10px;
  img 
  {
    width:15px;
  }
}
</style>
