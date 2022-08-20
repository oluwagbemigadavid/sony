<template>
  <div class="container">
    <img :src="images.bg" alt="" id="backgroundImg">
    <img :src="images.hpBg" alt="" id="HPBig">
    <div class="overlay"></div>
    <div class="section-01">
      <img :src="images.hp" alt="" id="hp">
      <img :src="images.optimizeIcon" alt="" id="optimizeIcon">
    </div>
    <div class="section-02">
      <div class="section-02-content">
        <h2>Sony WH-1000xm3</h2>
        <div id="text">
          <h4>2 Devices Connected</h4>
          <img :src="images.battery" alt="" id="battery" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import hpBg from '@/assets/HP-BG.png'
import hp from '@/assets/HPBG.png'
import bg from '@/assets/BG.png'
import optimizeIcon from '@/assets/optimize-Icon.png'
import battery from '@/assets/battery.png'

export default {
  name: 'HomeView',
  data () {
    return {
      images: {
        hpBg: hpBg,
        bg: bg,
        hp: hp,
        optimizeIcon: optimizeIcon,
        battery: battery
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.container {
  width: 100vw;
  height: 100vh;
  color: #fff;
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
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-top: 10%;
    #hp {
      width: 60%;
    }
    #optimizeIcon {
      position: absolute;
      //top: 35%;
      right: 15%;
      width: 60%;
    }
  }
  .section-02 {
    position: relative;
    .section-02-content {
      position: relative;
      margin-top: 5%;
      h2,h4 {
        margin: 2%;
      }
      #text {
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
        h4 {
          color: #969FA4;
        }
      }
    }
  }
}
</style>