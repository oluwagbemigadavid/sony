<template>
    <div class="sound-type-container" >
        <div class="view">
            <div class="mainContent">
                    <div class="switch" @click="view()">       
                        <div class="toggle-button-cover">
                            <div class="button-cover">
                                <div class="button r" id="button-1">
                                    <input type="checkbox" class="checkbox" checked>
                                    <div class="knobs"></div>
                                    <div class="layer"></div>
                                </div>
                            </div>
                        </div>
                    </div>
                <div class="top">
                    <h4>Adaptive Sound Control</h4>
                    <div class="menu">
                        <h3 class="stay" @click="staying()">Staying</h3>
                        <h3 class="transport active" @click="transport()">Transport</h3>
                        <h3 class="walk ">Walking</h3>
                        <h3 class="run ">Running</h3>
                        <h3 class="sleep ">Sleeping</h3>
                    </div>
                </div>
                        <img :src="images.bus" alt="" id="smolBus" @click="view()"/>
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
                    <h5 id="highlight">{{slider}}</h5>
                </div>
                <div class="slider">
                    <div class="range-input">
                        <input type="range" min="0" max="20" value="0" step="1" @input="Slider()">
                    </div>
                </div>
                <div class="focus">
                    <p id="focus">Focus on Voice</p>      
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
                </div>
                <p id="title"  @click="view()">Transport</p>
            </div>
            <div class="buttons">                
                <p id="done" @click="close()">Done</p>
                <p id="cancel" @click="close()">Cancel</p>
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
            },
            slider: 0,
            expanded: ''
        }
    },
    created() {
        if(this.slider == 0) {
            this.slider = 'Noise Cancelling'
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
        },
        Slider () {
            let rangeInput = document.querySelector(".range-input input");

            let step = parseFloat(rangeInput.value);

            this.slider = step
            if(this.slider == 0) {
                this.slider = 'Noise Cancelling'
            }
        },
        view () {
            document.querySelector('.view').classList.add('expanded')
            this.expanded = true
            this.$emit('expand', this.expanded)
            console.log(this.expanded)
        },
        close () {
            document.querySelector('.view').classList.remove('expanded')
            this.expanded = false
            this.$emit('expand', this.expanded)
            console.log(this.expanded)
        }
    }
}

</script>
<style lang="scss" scoped>
.sound-type-container { 
    position: relative;
    width: 40%;
    height: 100vh;
    z-index: 5;
    .view.expanded {
        width: 208%;
        height: 80%;
        margin: auto;
        margin-top: -230%;
        cursor: default;
        position: relative;
        transition: all .1s ease;
        z-index: 9;
        .mainContent {
            background-color: #1F2122;
            width: 120%;
            margin: auto;
            height: 70%;
            border-radius: 10px; 
            padding: 2% 0;  
            position: relative;     
                .switch {        
                    position: absolute;
                    transform: scale(.5); 
                    display: none;
                    z-index: 8;
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
            .top {
                position: relative; 
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: center;
                text-align: center;
                width: 95%;
                height: 18%;
                margin: 2%;
                margin-top: 5%;
                overflow: hidden;
                h4 {
                    color: #969FA4;
                    font-size: 14px;
                    font-weight: lighter;
                }
                .menu {
                    display: flex;
                    width: 90%;
                    height: 60%;
                    margin-top: 5%;
                    margin-bottom: -5%;
                    margin-left: 30%;
                    flex-direction: row;
                    position: relative;

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
            #smolBus {
                display: none;
            }
            .imageContainer {
                position: relative;
                height: 40%;
                margin-top: 5%;
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
                        top: 21%;
                    }
                    
                    #window2 {
                        width: 70px;
                        left: 60%;
                        top: 21%;
                    }
                    #wall {
                        width: 100%;
                        right: -5%;
                        top: -8%;
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
                margin: 0 auto;
                font-size: 18px;
                h5 {
                    font-weight: lighter;
                }
                #highlight {
                    position: absolute;
                    right: 0%;
                    color: #FFB375;
                }
            }
            .slider {
                display: flex;
                position: relative;
                width: 100%;
                .range-input {
                    position:absolute;
                    width: 100%;
                    top:5%;
                    left: 9%;
                    display:flex;
                    flex-direction: column;
                    }
                    .range-input input {
                    -webkit-appearance:none;
                    width:80%;
                    height:1px;
                    background:#969FA4;
                    border:none;
                    outline:none;
                    }
                    .range-input::before {
                    content: '';
                    -webkit-appearance:none;
                    position: absolute;
                    bottom: 0;
                    width:85%;
                    height:10px;
                    //background:#ff6a00;
                    border:none;
                    outline:none;
                    }
                    .range-input input::-webkit-slider-thumb {
                    -webkit-appearance:none;
                    width:20px;
                    height:20px;
                    background:#969FA4;
                    border:none;
                    border-radius:50%;
                    cursor: pointer;
                    }
                    .range-input input::-webkit-slider-thumb:hover {
                    background:#FFB375;
                    }
                    .range-input .value {
                    color:#FFB375;
                    text-align:center;
                    font-weight:600;
                    line-height:40px;
                    height:40px;
                    overflow:hidden;
                    margin-left:10px;
                    }
                    .range-input .value div {
                    transition:all 300ms ease-in-out;
                    }
            }
            .focus {
                display: flex;
                position: relative;
                width: 80%;
                font-weight: lighter;
                background-color: #303537;
                margin: 10% auto;
                text-align: left;
                border-radius: 10px;
                .switch {
                    display: block;                    
                    top: 50%;
                    right: 18%;
                }
                #focus {
                    padding:2% 5%;
                    width: 80%;
                }
            }
            
            #title {
                display: none;
            }
        }
        .buttons {            
            display: flex;
            flex-direction: row;
            position: relative;
            width: 120%;
            p {
                color: #000;
                background-color: #303537;
                padding: 5% 7%;
                width: 35%;
                border-radius: 10px;
                cursor: pointer;
            }
            #done {                
                background-color: #FFB375;
            }
            #cancel {
                color: #fff;
                position: absolute;
                right: 0%;
            }
        }
        
    }
    .view {
        width: 100%;
        height: 18%;
        margin: auto;
        font-weight: lighter;
        cursor: pointer;
        .mainContent {            
            padding: 10%;
            background-color: rgba(#1F2122, .7);
            width: 100%;
            margin: auto;
            height: 100%;
            border-radius: 10px;   
            position: relative;
            display: flex;
            flex-direction: column;
            justify-content: left;
            .switch{
                display: block;
                position: absolute;
                    transform: scale(.45); 
                    right: 26%;
                    top: 13%;
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
            .top {
                width: 80%;
                text-align: left;
                h4 {
                    margin: 0;
                    font-size: 15px;
                    font-weight: lighter;
                }
                .menu{
                    display: none;
                }
            }
            #smolBus { 
                width: 110px;
                margin-top: 10%;
            }
                .imageContainer {
                    .leftImages {
                        display: none;
                    }
                    .rightImages {
                        display: none;
                        #bus {
                            display: block;
                        }
                    }
                }
                .controlText {
                    display: none;
                }
                .slider {
                    display: none;
                }
                .focus {
                    display: none;
                }
            #title {
                font-size: 20px;
                text-align: left;
                font-weight: lighter;
            }
        }
        .buttons {
            display: none;
        }
    }
}
</style>