<template>
  <div class="heroSlider">
    <div class="heroOverlay"></div>
    <div class="heroContent contentPadding">
      <div class="heroStarsWrapper">
        
        <span class="heroStarsWrapper__start">
          <img  src="https://www.flaticon.com/svg/vstatic/svg/1828/1828884.svg?token=exp=1611861781~hmac=b095d56eca9d415a1f4ee0573a4959b5">
          5.6
        </span>
         <span class="heroStarsWrapper__date">
          2020
        </span>
      </div>
      <div class="heroContent__title">TENET</div>
      <div class="heroMinDesc">
        <div class="heroMinDesc__director">Director:<span style="color:yellow">John Doe</span></div>
        <div class="heroMinDesc__scenario">Scenario:<span style="color:yellow">Jane Doe</span></div>
      </div>
      <div class="heroContent__desc">Lorem ipsum dolor sit amet consectetur
         adipisicing elit. Placeat accusamus odit voluptas mollitia dolore vel
          harum, unde natus fugit, aliquam debitis inventore esse nobis modi!
           Quis numquam facilis consequuntur esse?</div>
           <button class="btn btn--main glow-btn">See more</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HeroSlider',
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.heroSlider
{
  width:100vw;
  height:100vh;
  background-image: url('https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fimages.wallpapersden.com%2Fimage%2Fdownload%2Ftenet-movie_68298_1920x1080.jpg&f=1&nofb=1');
  background-size: cover;
  background-position: center;
}
.heroOverlay
{
  position: absolute;
  z-index: 90;
  width:100vw;
  height:100vh;
  top:0px;
  left:0px;
  background:rgba(0,0,0,.8)
}
.heroContent
{
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: flex-start;
  position: relative;
  z-index: 100;
  top:35vh;
  width: 40vw;
  color:white;

}

.heroStarsWrapper
{
  font-size: 1.4em;
  padding-left: 5px;
  padding-bottom: 10px;
  img 
  {
    width:18px;
    height: auto;
  }
}
.heroStarsWrapper__date
{
  padding-left: 25px;
}
.heroContent__title
{
  font-size: 5em;
  text-align: left;
}

.heroMinDesc
{
 display: flex;
 padding-left: 5px;

}
.heroMinDesc__scenario
{
  padding-left: 25px;
}
.heroContent__desc
{
  
  font-size: 1.4em;
  text-align: left;
  padding:20px 0px 0px 5px;
}

.btn--main
{
  background:rgb(181, 3, 3);
  color:white;
  margin:25px 0px 0px 5px;
  font-size: 2em;
  width: 200px;
}

@media (max-width: 1300px) { 
  .heroContent
  {
    width:55vw;
  }
  
 }

 @media (max-width:890px) { 
    .heroContent
    {
      top:30vh;
       font-size: 1em;
    }
 }

  @media (max-width:690px) { 
    .heroContent
    {
      top:35vh;
      width: 95vw;
      font-size: .7em;
    }
 }
</style>
