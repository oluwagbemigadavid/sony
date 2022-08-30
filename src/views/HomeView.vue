<template>
  <div class="container">
    <div class="ImgContainer">
      <img :src="images.bg" alt="" id="backgroundImg">
      <img :src="images.hpBg" alt="" id="HPBig">
      <div class="overlay"></div>
    </div>
    <div class="section-01">
      <img :src="images.hp" alt="" id="hp">
      <img :src="images.optimizeIcon" alt="" id="optimizeIcon" @click="optimize()">
      <div class="hp">        
        <img :src="images.hprc" alt="" id="hprc">
        <div class="waves"></div>
      </div>
      
      <div class="opt-01">
        <div class="opt-cont">
          <h4>1/3</h4>
          <h2>Measuring Your Wearing Condition</h2>
          <p>Ear as always. Redo the process if you change the way you wear due to hairstyle change, etc.</p>
        </div>
      </div>
      <div class="opt-02">
        <div class="opt-cont">
          <h4>2/3</h4>
          <h2>Measuring Your Current Altitude</h2>
          <p>Calculatin the overall atmospheric pressure around you. Redo the prodess if you jump on a plane.</p>
        </div>
      </div>
      <div class="opt-03">
        <div class="opt-cont">
          <h4>3/3</h4>
          <h2>Analyzing Noise Cancelling Data</h2>
          <p>Almost there! Just puttingi everything together as Noise cancelling is optimally tailored to your taste.</p>
        </div>
      </div>


      <div class="optButton" @click="begOpt()" >
        <p id="status">Begin Optimization</p>
        <div class="progBar"></div>
      </div>
      <div class="sec-one-cont">
        <div class="section-01-content">
          <h2 class="txt">Noise Cancelling Optimizer</h2>
          <p class="txt">Wear headphones as you always would. If the ewearing condition changes, redo the process.</p>
          <div class="options">
            <div class="left">
              <img :src="images.ear" alt="">
              <div class="texts">
                <p id="highlight">On-Ear Personalization</p>
                <p>Not Set</p>
              </div>
            </div>
            <div class="right">
              <img :src="images.autoOpt" alt="" id="autoOpt">
              <div class="texts">
                <p id="highlight">Atmoshperic Optimization</p>
                <p>Set to 10 atm</p>
              </div>
            </div>
          </div>
        </div>
      </div>
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
import hprc from '@/assets/HP-Right Cup.png'
import bg from '@/assets/BG.png'
import ear from '@/assets/ear.png'
import autoOpt from '@/assets/AutoOpt.png'
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
                ear: ear,
                autoOpt: autoOpt,
                hprc:hprc,
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
          document.querySelector('.row-02').classList.add('index')
        } else {
          document.getElementById('play-music-component').style.display = 'block'
          document.querySelector('.underlay').classList.remove('active')
          document.querySelector('.row-02').classList.remove('index')
        }
      },
      state2() {
        if(this.elementState2) {
          document.getElementById('sound-type-component').style.display = 'none'
          document.querySelector('.underlay').classList.add('active')
          document.querySelector('.row-02').classList.add('index')
        } else {
          document.getElementById('sound-type-component').style.display = 'block'
          document.querySelector('.underlay').classList.remove('active')
          document.querySelector('.row-02').classList.remove('index')
        }
      },
      optimize () {
        document.querySelector('.section-01').classList.add('optimize')
        document.querySelector('.section-02').classList.add('opt')
        document.querySelector('.ImgContainer').classList.add('optim')
        document.querySelector('.section-01-content').style.display = 'block'
        setTimeout(()=> document.getElementById('optimizeIcon').style.zIndex = '0', 200)
      },
      begOpt () {
        document.querySelector('.section-01-content').classList.add('begOpt')
        setTimeout(()=> document.querySelector('.section-01-content').style.display = 'none', 600)
        document.querySelector('.section-01').classList.add('optimizing')

        var speed = 0
        var prog = document.querySelector('.progBar')
        var timer = null
        timer = setInterval (() => {
          if(speed >= 100) {
            clearInterval(timer)
          } else {
            prog.style.width = speed + '%'
            speed++
            document.getElementById('status').style.fontStyle = 'italic'
            if ( speed < 50){
              document.getElementById('status').innerHTML = 'Optimizing...'
            }
            if ( speed == 50){
              document.getElementById('status').innerHTML = 'Almost there...'
            }
            if ( speed == 80){
              document.getElementById('status').innerHTML = 'Finishing...'
            }
          }
        }, 54)

        setTimeout(()=> {
          document.querySelector('.opt-01').classList.add('show')   
        }, 500)
        setTimeout(()=> {
          document.querySelector('.opt-01').classList.remove('show') 
          document.querySelector('.opt-02').classList.add('show')   
        }, 2000)
        setTimeout(()=> {
          document.querySelector('.opt-02').classList.remove('show') 
          document.querySelector('.opt-03').classList.add('show')   
        }, 4000)
        setTimeout(()=> {
          document.querySelector('.opt-03').classList.remove('show')   
          document.querySelector('.section-01').classList.remove('optimize')
          document.querySelector('.section-02').classList.remove('opt')
          document.querySelector('.ImgContainer').classList.remove('optim')
          document.querySelector('.section-01-content').classList.remove('begOpt')
          document.querySelector('.section-01').classList.remove('optimizing')
          document.getElementById('optimizeIcon').style.zIndex = '4'
        }, 5500)
        setTimeout(()=> {        
          document.getElementById('status').style.fontStyle = 'normal'
          document.getElementById('status').innerHTML = 'Begin Optimization'   
          document.querySelector('.progBar').style.width = '0%'
        }, 5600)
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
@keyframes disappear {
  0% {
    opacity: 1;
  }
  50% {
    opacity: .2;
  }
  100% {
    opacity: 0;
  }
}
@keyframes grow {
  0% {
    transform: scale(1);
  }
  100% {
    transform: scale(2);
  }
}
@keyframes floatDown {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0;
    margin-top: 50%;
  }
}
@keyframes wave {
  0% {
    transform: scale(1) skewX(10deg);
    //transform-origin: 42% 50%;
    opacity: .3;
    background: rgb(0, 0, 0);
  }
  50% {
    transform: scale(2) skewX(10deg);    
    width: 80%;
    left: 25%;
    opacity: .3;
    background: rgb(130, 130, 130);
  }
  100% {
    transform: scale(5) skewX(10deg);
    width: 100%;
    left: 0%;
    opacity: 0;
    background: rgb(194, 194, 194);
  }
}
@keyframes appear {
  0% {
    opacity: 0;
    transform: scale(0);
  }
  35% {
    opacity: 0;
    transform: scale(1);
    margin-top: -30%;
  }
  100% {
    opacity: 1;
    margin-top: -30%;
    transform: scale(1);
  }
}
@keyframes show {
  0% {
    opacity: 0;
  }
  75% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
.container {
  width: 100vw;
  height: 100vh;
  color: #fff;
  position: relative;
  overflow: hidden;
  -webkit-tap-highlight-color: transparent;
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
        //display: none;
        opacity: 1;
        transition: opacity 450ms ease-out;
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
  .ImgContainer.optim {
    #HPBig {
        opacity: 0;
        display: none;
        transition: opacity 450ms ease-out;      
    }
  }
  .section-01 {
    position: relative;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 40%;
    transition: height 1s;
    .hp {
      display: none;
    }
    .section-01-content {
      display: none;
    }
    #hp {
      width: 50%;
      margin-top: 10%;
      transform: scale(1);
      opacity: 1;
      transition: all 1s ease-in;
      position: absolute;
      top: 0;
      z-index: 2;
    }
    #optimizeIcon {
      position: absolute;
      right: 15%;
      width: 60%;
      margin-top: 20%;
      top: 0%;
      z-index: 2;
      opacity: 1;
      transition: all 1s;
      cursor: pointer;
      -webkit-tap-highlight-color: transparent;
    }
    .optButton {
      display: none;
    }
  }
    .opt-01, .opt-02, .opt-03 {
      position: absolute;
      bottom: 12%;
      display: none;
      .opt-cont{
        -webkit-tap-highlight-color: transparent;
      }
    }
    .opt-01.show {
      display: flex;
      flex-direction: column;
      justify-content: center;
      .opt-cont {
        animation: show 500ms ease-in;
        h4 {
          color: #FFB375;
        }
        h2 {
          width: 60%;
          margin: 2% auto;
          color: #fff;
        }
        p {
          width: 80%;
          margin: auto;
          color: #969FA4;
        }

      }
    }
    .opt-02.show {
      display: flex;
      flex-direction: column;
      justify-content: center;
      .opt-cont {
        animation: show 500ms ease-in;
        h4 {
          color: #FFB375;
        }
        h2 {
          width: 60%;
          margin: 2% auto;
          color: #fff;
        }
        p {
          width: 80%;
          margin: auto;
          color: #969FA4;
        }

      }
    }
    .opt-03.show {
      display: flex;
      flex-direction: column;
      justify-content: center;
      .opt-cont {
        animation: show 500ms ease-in;
        h4 {
          color: #FFB375;
        }
        h2 {
          width: 60%;
          margin: 2% auto;
          color: #fff;
        }
        p {
          width: 80%;
          margin: auto;
          color: #969FA4;
        }

      }
    }
  .section-01.optimize {
    height: 100vh;
    transition: height 1s;
    #hp {
      margin-top: -35%;
      margin-left: 45%;
      transform: scale(4);
      opacity: 0;
      transition: all 1s ease-in;
    }
    #optimizeIcon {
      opacity: 0;
      transition: all 1s;
    }
    .hp {
      display: flex;
      position: absolute;
      top: 0;
      justify-content: center;
      #hprc {
        position: relative;
        margin-top: -30%;
        transform: scale(1);
        transition: all 1s;
        animation: appear 1.5s ease-out;
        z-index: 1;
      }
      .waves {
        display: none;
        position: absolute;
        width: 35%;
        height: 35%;
        left: 45%;
        border-radius: 180px;
        opacity: .5;
        z-index: 2;
        top: 45%;
        transform: skewX(10deg);
        -webkit-tap-highlight-color: transparent;
      }
    }
      .optButton {
        display: flex;
        position: absolute;
        width: 80%;
        padding: 5%;
        border-radius: 10px;
        background-color: #FFB375;
        bottom: 2%;
        left: 5%; 
        margin-top: 100%;
        animation: show 1s ease-in;
        cursor: pointer;
        text-align: center;
        -webkit-tap-highlight-color: transparent;
        p {
          margin: 0;
          width: 100%;
          color: #000;
          font-weight: bold;
          text-align: center;
        }
        .progBar{
          width: 0%;
          bottom: 0%;
          left: 0%; 
          border-radius: 10px;
          height: 100%;
          position: absolute;
          background-color: rgba(#ffffff, .2);
          -webkit-tap-highlight-color: transparent;
        }
      }
      .sec-one-cont {
        overflow: hidden;
        position: relative;
        margin-top: 100%;
        height: 30%;
        -webkit-tap-highlight-color: transparent;
      }
    .section-01-content {
      display: block;
      animation: show 1s ease-in;
      -webkit-tap-highlight-color: transparent;
      p {
        color: #969FA4;
        width: 75%;
        font-size: 15px;
        margin: 0 auto;
        font-weight: lighter;
        -webkit-tap-highlight-color: transparent;
      }
      .options {
        display: flex;
        .left {
          margin: 5% 0% 5% 5%;
          width: 50%;
          padding: 5%;
          border-radius: 10px;
          text-align: left;
          display: flex;
          background-color: #1F2122;
          -webkit-tap-highlight-color: transparent;
          cursor: pointer;
          img {
            width: 18%;
            height: 40%;
          }
          .texts {
            p {
              font-size: 14px;
            }
            #highlight {
              color: #fff;
              margin-bottom: 10%;
            }
          }
        }
        .right {
          margin: 5% 5% 5% 5%;
          width: 50%;
          padding: 5%;
          border-radius: 10px;
          text-align: left;
          display: flex;
          background-color: #1F2122;
          cursor: pointer;
          -webkit-tap-highlight-color: transparent;
          img {
            width: 18%;
            height: 30%;
          }
          .texts {
            p {
              font-size: 12px;
              color: #FFB375;
            }
            #highlight {
              color: #fff;
              font-size: 14px;
              margin-bottom: 10%;
            }
          }
        }
      }
    }
    .section-01-content.begOpt {
      animation: floatDown 600ms ease-out ;
    }
  }
  .section-01.optimizing {
    .hp {
      #hprc {
        position: relative;
        margin-top: -18%;
        transform: scale(1.5);
        transition: all 1s;
        z-index: 1;
      }
      .waves {
        display: flex;
        position: absolute;
        width: 35%;
        height: 45%;
        left: 50%;
        border-radius: 50%;
        animation: wave 2s;
        animation-delay: 500ms;
        opacity: .5;
        z-index: 2;
        top: 52%;
        transform: skewX(10deg);
      }
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
  .section-02.opt {
    animation: disappear 1s ease-out;
    opacity: 0;
    transition: opacity 1s;
  }
  .section-02 {
    position: relative;
    opacity: 1;
    transition: opacity 1s;
    .section-02-content {
      position: relative;
      margin-top: 0%;
      -webkit-tap-highlight-color: transparent;
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
        -webkit-tap-highlight-color: transparent;
        #play-music-component {
          margin-left: 12%;
          -webkit-tap-highlight-color: transparent;
        }
      }
      .row-02.index {
        z-index: 6;
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
        z-index: 8;
        -webkit-tap-highlight-color: transparent;
        .row-02-Container {
          text-align: left;
          color: #969FA4;
          padding: 2%;
          -webkit-tap-highlight-color: transparent;
          p {
            margin: 5% 5% ;
          }
          ::-webkit-scrollbar{
            height: 0px;
            width: 0px;
            background: gray;
          }
          .slidingMenu {
            position: relative;
            overflow-x: scroll;
            -webkit-tap-highlight-color: transparent;
            .menuContents {
              display: flex;
              width: 165%;
              margin: 0 0 0 -45%;
              -webkit-tap-highlight-color: transparent;
              p {
                font-size: 20px;
                font-weight: lighter;
                margin: 0 2%;
                cursor: pointer;
                -webkit-tap-highlight-color: transparent;
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
            -webkit-tap-highlight-color: transparent;
          }
        }
      }
    }
  }
}
</style>