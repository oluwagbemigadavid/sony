<template>
  <div class="container">
    <div class="ImgContainer">
      <img :src="images.bg" alt="" id="backgroundImg">
      <img :src="images.hpBg" alt="" id="HPBig">
      <div class="overlay"></div>
    </div>
    <div class="section-01">
      <img :src="images.hp" alt="" id="hp">
      <img :src="images.optimizeIcon" alt="" id="optimizeIcon">
    </div>
    <div class="underlay"></div>
    <div class="section-02">
      <div class="section-02-content">
        <h2>Sony WH-1000xm3</h2>
        <div id="text">
          <h4>2 Devices Connected</h4>
          <img :src="images.battery" alt="" id="battery" />
        </div>
        <div class="row-01">
          <SoundTypeComponent id="sound-type-component" @expand="getState" @click="state()"/>
          <PlayMusicComponet id="play-music-component" @expand2="getState2" @click="state2()"/>
        </div>
        <div class="row-02">
          <div class="row-02-Container">
            <p>3D sound Equalizer</p>
            <div class="slidingMenu">
              <div class="menuContents">
                <p id="1" class="eq  " @click="activeEq(5, 1)">Electronic</p>
                <p id="2" class="eq " @click="activeEq(-20, 2)">Church</p>
                <p id="3" class="eq active" @click="activeEq(-45, 3)">Bass Boost</p>
                <p id="4" class="eq " @click="activeEq(-70, 4)">Classical</p>
                <p id="5" class="eq " @click="activeEq(-95, 5)">Concert</p>
                <p id="6" class="eq " @click="activeEq(-100, 6)">Hall</p>
              </div>
            </div>
            <img :src="images.eq" alt="" />
          </div>
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
import eq from '@/assets/Eq.png'
import SoundTypeComponent from '@/components/SoundTypeComponent.vue'
import PlayMusicComponet from '@/components/PlayMusicComponet.vue'


export default {
    name: "HomeView",
    components: { SoundTypeComponent, PlayMusicComponet },
    data() {
        return {
            images: {
                hpBg: hpBg,
                bg: bg,
                hp: hp,
                eq: eq,
                optimizeIcon: optimizeIcon,
                battery: battery
            },
            elementState: '',
            elementState2: ''
        };
    },
    created () {     
    },
    methods: {
      getState (value) {
        this.elementState = value
      },
      getState2 (value) {
        this.elementState2 = value
      },
      state() {
        if(this.elementState) {
          document.getElementById('play-music-component').style.display = 'none'
          document.querySelector('.underlay').classList.add('active')
        } else {
          document.getElementById('play-music-component').style.display = 'block'
          document.querySelector('.underlay').classList.remove('active')
        }
      },
      state2() {
        if(this.elementState2) {
          document.getElementById('sound-type-component').style.display = 'none'
          document.querySelector('.underlay').classList.add('active')
        } else {
          document.getElementById('sound-type-component').style.display = 'block'
          document.querySelector('.underlay').classList.remove('active')
        }
      },
      activeEq (value, id) {
        document.querySelector('.menuContents').style.margin = ` 0 0 0 ${value}%` 
        //var buttons = document.getElementsByClassName('eq')
        if(id == 1) {
          document.getElementById('1').style.color = '#FFB375'
          document.getElementById('2').style.color = '#969FA4'
          document.getElementById('3').style.color = '#969FA4'
          document.getElementById('4').style.color = '#969FA4'
          document.getElementById('5').style.color = '#969FA4'
          document.getElementById('6').style.color = '#969FA4'
        } else if (id == 2) {
          document.getElementById('1').style.color = '#969FA4'
          document.getElementById('2').style.color = '#FFB375'
          document.getElementById('3').style.color = '#969FA4'
          document.getElementById('4').style.color = '#969FA4'
          document.getElementById('5').style.color = '#969FA4'
          document.getElementById('6').style.color = '#969FA4'
        } else if (id == 3) {
          document.getElementById('1').style.color = '#969FA4'
          document.getElementById('2').style.color = '#969FA4'
          document.getElementById('3').style.color = '#FFB375'
          document.getElementById('4').style.color = '#969FA4'
          document.getElementById('5').style.color = '#969FA4'
          document.getElementById('6').style.color = '#969FA4'
        } else if (id == 4) {
          document.getElementById('1').style.color = '#969FA4'
          document.getElementById('2').style.color = '#969FA4'
          document.getElementById('3').style.color = '#969FA4'
          document.getElementById('4').style.color = '#FFB375'
          document.getElementById('5').style.color = '#969FA4'
          document.getElementById('6').style.color = '#969FA4'
        } else if (id == 5) {
          document.getElementById('1').style.color = '#969FA4'
          document.getElementById('2').style.color = '#969FA4'
          document.getElementById('3').style.color = '#969FA4'
          document.getElementById('4').style.color = '#969FA4'
          document.getElementById('5').style.color = '#FFB375'
          document.getElementById('6').style.color = '#969FA4'
        } else if (id == 6) {
          document.getElementById('1').style.color = '#969FA4'
          document.getElementById('2').style.color = '#969FA4'
          document.getElementById('3').style.color = '#969FA4'
          document.getElementById('4').style.color = '#969FA4'
          document.getElementById('5').style.color = '#969FA4'
          document.getElementById('6').style.color = '#FFB375'
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
    .ImgContainer {
      width: 100vw;
      height: 100%;
      position: absolute;
      top: 0;
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
        top: -35%;
        transform: scale(1);
      }
      .overlay {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 20%;
        background: linear-gradient( to bottom, rgba(#1F2122, 1) 5%, rgba(#1F2122, 0));
        z-index: 1;
      }
    }
  .section-01 {
    position: relative;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-top: 0%;
    #hp {
      width: 50%;
      margin-top: 10%;
    }
    #optimizeIcon {
      position: absolute;
      //top: 35%;
      right: 15%;
      width: 60%;
    }
  }
  .underlay {
    width: 100vw;
    height: 100vh;
    position: fixed;
    top: 0;
    left: 0;
    z-index: 7;
    background-color: rgba(#000, .7);
    display: none;
    
  }
  .underlay.active {
    display: block;
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
      .row-01 {
        width: 94%;
        margin: auto;
        margin-top: 5%;
        margin-left: 3%;
        display: flex;
        justify-content: left;
        position: absolute;
        z-index: 7;
        #play-music-component {
          margin-left: 12%;
        }
      }
      .row-02 {
        width: 94%;
        margin: auto;
        position: relative;
        margin-top: 60%;
        background-color: #1F2122;
        border-top-left-radius: 10px;
        border-top-right-radius: 10px;
        overflow: hidden;
        z-index: 6;
        .row-02-Container {
          text-align: left;
          color: #969FA4;
          padding: 2%;
          p {
            margin: 5% 5% ;
          }
          .slidingMenu {
            position: relative;
            overflow-x: scroll;
            .menuContents {
              display: flex;
              width: 165%;
              margin: 0 0 0 -45%;
              p {
                font-size: 20px;
                font-weight: lighter;
                margin: 0 2%;
                cursor: pointer;
              }
              .active {
                color: #FFB375;
              }
            }
          }
          img {
            margin-top: 5%;
            width: 105%;
            margin-left: -2%;
          }
        }
      }
    }
  }
}
</style>