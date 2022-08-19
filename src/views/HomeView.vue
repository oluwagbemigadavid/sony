<template>
  <div class="container">
    <img :src="images.bg" alt="" id="backgroundImg">
    <img :src="images.hpBg" alt="" id="HPBig">
    <div class="overlay"></div>
    <div class="section-01">
      <img :src="images.hp" alt="" id="hp">
    </div>
  </div>
</template>

<script>
import hpBg from '@/assets/HP-BG.png'
import hp from '@/assets/HPBG.png'
import bg from '@/assets/BG.png'

export default {
  name: 'HomeView',
  data () {
    return {
      images: {
        hpBg: hpBg,
        bg: bg,
        hp: hp
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.container {
  width: 100vw;
  height: 100vh;
  position: relative;
  overflow: hidden;
  #backgroundImg  {
    position: fixed;
    width: 100vw;
    height: 100vh;
    top: 0;
    left: 0;
    z-index: -1;
  }
  #HPBig  {
    height: 100%;
    position: absolute;
    left: -35%;
    top: -40%;
    transform: scale(1);
  }
  .overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 20%;
    background: linear-gradient( to bottom, rgba(#000, 1) 5%, rgba(#000, 0));
    z-index: 2;
  }
  .section-01 {
    position: relative;
    #hp {
      margin-top: 20%;
      transform: scale(1.2);
    }
  }
}
</style>