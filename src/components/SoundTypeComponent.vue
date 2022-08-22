<template>
    <div class="sound-type-container">
        <div class="view expanded">
            <div class="mainContent">
                <div class="top">
                    <h4>Adaptive Sound Control</h4>
                    <div class="switch">       
                        <div class="toggle-button-cover">
                            <div class="button-cover">
                                <div class="button r" id="button-1">
                                    <input type="checkbox" class="checkbox">
                                    <div class="knobs"></div>
                                    <div class="layer"></div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="menu">
                        <h3 class="stay" @click="staying()">Staying</h3>
                        <h3 class="transport active" @click="transport()">Transport</h3>
                        <h3 class="walk ">Walking</h3>
                        <h3 class="run ">Running</h3>
                        <h3 class="sleep ">Sleeping</h3>
                    </div>
                </div>
                <div class="imageContainer  ">     
                    <div class="leftImages">
                        <img :src="images.wall" alt="" id="wall"/>  
                        <img :src="images.window" alt="" id="window1"/> 
                        <img :src="images.window" alt="" id="window2"/>
                        <img :src="images.tv" alt="" id="tv"/> 
                        <img :src="images.person" alt="" id="person"/> 
                    </div>
                    <div class="rightImages ">   
                        <img :src="images.tree" alt="" id="fisrtTree"/>
                        <img :src="images.tree" alt="" id="smallTree" />
                        <img :src="images.star" alt="" id="star3" />
                        <img :src="images.cloud" alt="" id="cloud"/>
                        <img :src="images.star" alt="" id="star2" />
                        <img :src="images.star" alt="" id="star1" />
                        <img :src="images.tree" alt="" id="lastTree"/>
                        <img :src="images.bus" alt="" id="bus"/>
                    </div>                        
                </div>
                <div class="controlText">
                    <h5>Ambient Sound</h5>
                    <h5 id="highlight">Noise Cancelling</h5>
                </div>
            </div>
            
        </div>
    </div>
</template>

<script>
import bus from '@/assets/Bus-Transport.png'
import cloud from '@/assets/Cloud-1.png'
import overlay from '@/assets/Overlay.png'
import person from '@/assets/Person.png'
import tv from '@/assets/TV.png'
import window from '@/assets/window.png'
import wall from '@/assets/Wall.png'
import star from '@/assets/Star-1.png'
import tree from '@/assets/Tree-1.png'

export default {
    data () {
        return {
            images: {
                bus: bus,
                cloud: cloud,
                overlay: overlay,
                person: person,
                tv: tv,
                window: window,
                star: star,
                tree: tree,
                wall: wall
            }
        }
    },
    methods: {
        staying () {
            document.querySelector('.imageContainer').classList.add('staying')
            document.querySelector('.stay').classList.add('active')
            document.querySelector('.transport').classList.remove('active')
            document.querySelector('.menu').style.transform = `translateX(23%)`
            document.querySelector('.menu').style.transition = `transform 250ms ease-in-out`
        },
        transport () {
            document.querySelector('.imageContainer').classList.remove('staying')
            document.querySelector('.stay').classList.remove('active')
            document.querySelector('.transport').classList.add('active')
            document.querySelector('.menu').style.transform = `translateX(0%)`
            document.querySelector('.menu').style.transition = `transform 250ms ease-in-out`
        }
    }
}

</script>
<style lang="scss" scoped>
.sound-type-container { 
    position: relative;
    height: 100vh;
    z-index: 8;
    .view.expanded {
        width: 94%;
        height: 70%;
        margin: auto;
        margin-top: -85%;
        .mainContent {
            background-color: #1F2122;
            width: 100%;
            margin: auto;
            height: 70%;
            border-radius: 10px;
            .top {
                position: relative; 
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: center;
                //overflow: hidden;
                h4 {
                    color: #969FA4;
                    font-size: 14px;
                    font-weight: lighter;
                }
                .switch {        
                    position: absolute;
                    transform: scale(.5);
                    display: none;        
                    .toggle-button-cover
                    {
                        position: relative;
                        box-sizing: border-box;
                    }

                    .button-cover:before
                    {
                        counter-increment: button-counter;
                        content: '';
                        position: absolute;
                        right: 0;
                        bottom: 0;
                        color: #969FA4;
                        font-size: 12px;
                        line-height: 1;
                        padding: 5px;
                    }

                    .button-cover, .knobs, .layer
                    {
                        position: absolute;
                        top: 0;
                        right: 0;
                        bottom: 0;
                        left: 0;
                    }

                    .button
                    {
                        position: relative;
                        top: 50%;
                        width: 74px;
                        height: 36px;
                        margin: -20px auto 0 auto;
                        overflow: hidden;
                    }

                    .button.r, .button.r .layer
                    {
                        border-radius: 100px;
                    }

                    .button.b2
                    {
                        border-radius: 2px;
                    }

                    .checkbox
                    {
                        position: relative;
                        width: 100%;
                        height: 100%;
                        padding: 0;
                        margin: 0;
                        opacity: 0;
                        cursor: pointer;
                        z-index: 3;
                    }

                    .knobs
                    {
                        z-index: 2;
                    }

                    .layer
                    {
                        width: 100%;
                        background-color: #969FA4;
                        transition: 0.3s ease all;
                        z-index: 1;
                    }

                    /* Button 1 */
                    #button-1 .knobs:before
                    {
                        content: '';
                        position: absolute;
                        top: 4px;
                        left: 4px;
                        width: 20px;
                        height: 10px;
                        font-size: 10px;
                        font-weight: bold;
                        text-align: center;
                        line-height: 1;
                        padding: 9px 4px;
                        background-color: #fff;
                        border-radius: 50%;
                        transition: 0.3s cubic-bezier(0.18, 0.89, 0.35, 1.15) all;
                    }

                    #button-1 .checkbox:checked + .knobs:before
                    {
                        content: '';
                        left: 42px;
                        background-color: #fff;
                    }

                    #button-1 .checkbox:checked ~ .layer
                    {
                        background-color: #FFB375;
                    }

                    #button-1 .knobs, #button-1 .knobs:before, #button-1 .layer
                    {
                        transition: 0.3s ease all;
                    }
                }
                .menu {
                    display: flex;
                    width: 90%;
                    height: 60%;
                    margin-left: 30%;
                    flex-direction: row;

                    h3 {
                        margin: 0 3%;
                        font-weight: lighter;
                        cursor: pointer;
                    }
                    .active {
                        color: #FFB375;
                    }
                }
            }
            .imageContainer {
                position: relative;
                height: 40%;
                margin-top: 10%;
                overflow: hidden;
                img {
                    position: absolute;
                    width: 100px;
                }
                .leftImages {
                    display: flex;
                    flex-direction: row;
                    height: 100%;
                    width: 100%;
                    position: absolute;
                    left: -90%;
                    z-index: 9;
                    transition: left .5s;

                    #window1 {
                        width: 70px;
                        left: 17%;
                        top: 20%;
                    }
                    
                    #window2 {
                        width: 70px;
                        left: 60%;
                        top: 20%;
                    }
                    #wall {
                        width: 100%;
                        right: -5%;
                        top: -10.5%;
                    }
                    #tv {
                        right: 11%;
                    }
                    #person {
                        width: 110px;
                        bottom: 0;
                        left: 36%;
                    }
                }
                .rightImages {
                    display: flex;
                    flex-direction: row;
                    bottom: 0;
                    left: 0;
                    height: 100%;
                    width: 100%;
                    position: absolute;
                    transition: left .5s;
                    #fisrtTree {
                        bottom: 0;
                        left: -6%;
                    }
                    #smallTree {
                        width: 60px;
                        bottom: 0;
                        left: 17%
                    }
                    #cloud {
                        width: 50px;
                        left: 50%;
                        top: 5%;
                    }
                    #star3 {
                        width: 10px;
                        left: 25%;
                        top: 27%;
                    }
                    #star2 {
                        width: 10px;
                        left: 65%;
                    }
                    #star1 {
                        width: 10px;
                        top: 27%;
                        left: 78%;
                    }
                    #lastTree {
                        bottom: 0;
                        right: -15.3%;
                    }
                    #bus {
                        width: 180px;
                        bottom: 0%;
                        left: 25%;
                        margin: auto;
                    }
                }
            }
            .imageContainer.staying {
                .rightImages {
                    left: 77%;
                    transition: all .5s;
                }
                .leftImages {
                    left: 0;
                    transition: all .5s;
                }
            }
            .controlText {
                display: flex;
                position: relative;
                width: 80%;
                margin: auto;
                h5 {
                    font-weight: lighter;
                }
                #highlight {
                    position: absolute;
                    right: 0%;
                    color: #FFB375;
                }
            }

        }
        
    }
}
</style>