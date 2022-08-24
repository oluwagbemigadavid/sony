<template>
    <div class="play-music-container">
        <div class="view2">
            <div class="main-content">                
                <div class="content">
                    <div class="displayImg">
                        <div class="image">
                            <img :src="items[activeIdPreview].img" alt="" id="img">
                        </div>
                        <div class="overlay"> </div>
                        <div v-for="(item) in items" :key="item.id"  class="topImg">
                            <div v-if="item.id == activeId">
                                <div class="img">
                                    <img :src="item.img" alt="" id="displayImage" class="displayImage">
                                </div>
                                <div class="row-one" @click="view()">
                                    <p>Now Playing</p>
                                </div>
                                <div class="row-two" @click="view()">
                                    <h2 id="genre">{{ item.feat }} - {{ item.genre}}</h2>
                                        <p id="name">{{ item.feat }}</p>
                                        
                                </div>
                                <div class="row-three">
                                    <p>{{ item.feat}}, {{ item.name}}</p>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="row-four">  
                        <div class="slider2">
                            <div class="range-input2">
                                <input type="range" min="0" max="255" value="0" step="1" @input="slider()">
                            </div>
                            <div class="texts">
                                <p>{{start}}</p>
                                <p id="stop">{{stop}}</p>
                            </div>
                        </div>
                    </div>
                    <div class="row-five" @click="view()">
                        <div class="icons">
                            <i class="fa-solid fa-backward-step" id="prev" @click="next('left')"></i>
                            <i class="fa-solid fa-play"></i>
                            <i class="fa-solid fa-forward-step" id="next" @click="next('right')"></i>
                        </div>
                    </div>
                </div>
            </div>
            <div class="buttons">                
                <p id="done" @click="close()"><i class="fa-brands fa-spotify"></i>Open in Spotify</p>
                <p id="cancel" @click="close()">Cancel</p>
            </div>
        </div>
    </div>
</template>

<script>


export default  {
    data () {
        return {
            items: [
                {
                    id: 1,
                    name: 'Beyonce',
                    genre: 'Bants',
                    age: 40,
                    img: 'https://pbs.twimg.com/media/D4VlVh1XkAEqGet?format=jpg&name=small',
                    feat: 'Lemonade',
                    secImg: 'https://pbs.twimg.com/media/Df1_x4gWsAEvIpR?format=jpg&name=4096x4096',
                    pop: 'Top Charts',
                    duration: 225
                },
                {
                    id: 2,
                    name: 'Koning David',
                    genre: 'Keyss',
                    age: 22,
                    img: 'https://pbs.twimg.com/media/FNCDVp4XwAoN5gm?format=jpg&name=large',
                    feat: 'Dance all Night',
                    secImg: 'https://images.unsplash.com/photo-1599790772272-d1425cd3242e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=464&q=80',
                    Pop: 'Universasl',
                    duration: 258
                },
                {
                    id: 3,
                    name: 'Beyonce',
                    genre: 'Bants',
                    age: 40,
                    img: 'https://pbs.twimg.com/media/D4VlVh1XkAEqGet?format=jpg&name=small',
                    feat: 'Lemonade',
                    secImg: 'https://pbs.twimg.com/media/Df1_x4gWsAEvIpR?format=jpg&name=4096x4096',
                    pop: 'Top Charts',
                    duration: 225
                },
                {
                    id: 4,
                    name: 'Koning David',
                    genre: 'Keyss',
                    age: 22,
                    img: 'https://pbs.twimg.com/media/FNCDVp4XwAoN5gm?format=jpg&name=large',
                    feat: 'Dance all Night',
                    secImg: 'https://images.unsplash.com/photo-1599790772272-d1425cd3242e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=464&q=80',
                    Pop: 'Universasl',
                    duration: 258
                },
            ],
            start: 0,
            stop: 0,
            activeId: 2,
            activeIdPreview: 0,
            expanded: ''
        }
    },
    methods: {        
        slider () {
            let rangeInput = document.querySelector(".range-input2 input");

            this.start = parseFloat(rangeInput.value);
            console.log(this.start)
        },
        view () {
            document.querySelector('.view2').classList.add('expanded2')
            this.expanded = true
            this.$emit('expand', this.expanded)
            console.log(this.expanded)
        },
        close () {
            document.querySelector('.view2').classList.remove('expanded2')
            this.expanded = false
            this.$emit('expand', this.expanded)
            console.log(this.expanded)
        },
        next (direction) {
            if (direction == 'right') {
                if(this.activeId == 4 && this.activeIdPreview == 2) {
                    setTimeout(() => {
                        this.activeId = 4 
                        this.activeIdPreview = 2
                    }, 20)
                } else {
                    ++this.activeId
                    ++this.activeIdPreview
                    console.log(this.activeId)
                }
            } else if (direction == 'left') {                
                if(this.activeId == 2 && this.activeIdPreview == 0) {
                    setTimeout(() => {
                        this.activeId = 2 
                        this.activeIdPreview = 0
                    }, 20)
                } else {
                    --this.activeId
                    --this.activeIdPreview
                    console.log(this.activeId)
                }
            }
            
        }
    }
}
</script>

<style lang="scss" scoped>
@keyframes topLeft {
    0% {
        transform: translateX(0%) translateY(0%);
    }
    100% {
        transform: translateX(-100%) translateY(-100%);
    }
    
}
@keyframes bottomLeft {
    0% {
        transform: translateX(100%) translateY(100%);
    }
    100% {
        transform: translateX(0%) translateY(0%);
    }
    
}
    .play-music-container {        
        position: relative;
        width: 40%;
        height: 100vh;
        z-index: 5;
        .view2 {            
            width: 100%;
            height: 18%;
            margin: auto;
            font-weight: lighter;
            cursor: pointer;
            .main-content {            
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
                .content {
                    .displayImg {
                        .image {
                            display: none;
                        }
                        .topImg {
                            .img {
                                display: none;
                            }
                            .row-one {
                                p {
                                    margin: 0;
                                    font-weight: lighter;
                                    text-align: left;
                                }
                            }
                            .row-two {
                                #name{ 
                                    color: #FFB375;
                                    margin: 0;
                                    font-weight: lighter;
                                    text-align: left;
                                }
                                #genre { 
                                    font-weight: lighter;
                                    text-align: left;
                                    margin: 10% 0; 
                                    font-size: 20px;
                                    height: 10%;
                                    width: 90%;
                                }
                                #age {
                                    display: none;
                                }
                            }
                            .row-three {
                                display: none;
                            }
                        }
                    }
                }
                .row-four {
                    display: none
                }
                .row-five {
                    margin: 10% 0 0;
                    .icons {
                        display: flex;
                        justify-content: center;
                        gap: 20%;
                        i {
                            width: 50%;
                            margin: 0;
                            font-size: 28px;
                        }
                        #prev {
                            text-align: left;
                        }
                        #next {
                            text-align: right;
                        }
                    }
                }
            }
            .buttons {
                display: none;
            }
        }
        .view2.expanded2 {      
            width: 208%;
            height: 80%;
            margin: auto;
            margin-top: -230%;
            margin-left: -130%;
            cursor: default;
            position: relative;
            transition: all .1s ease;
            z-index: 9;
            .main-content {            
                padding: 10%;
                background-color: rgba(#1F2122, 1);
                width: 100%;
                margin: auto;
                height: 70%;
                border-radius: 10px;   
                position: relative;
                display: flex;
                flex-direction: column;
                justify-content: left;
                overflow: hidden;
                .content {
                    .displayImg {
                        overflow: hidden;
                        .image {
                            display: block;
                        }
                        #img {
                            position: absolute;
                            width: 100%;
                            height: 45vh;
                            top: 0;
                            left: 0;
                            border-radius: 10px;
                            animation: topLeft 450ms ease-out;
                        }
                                .overlay {
                                    position: absolute;
                                    width: 102%;
                                    height: 50vh;
                                    left: 0%;
                                    top: 0;
                                    z-index: 1;
                                    background: linear-gradient(to top, rgba(#1F2122, 1) 10%, rgba(#1F2122, 0));
                                }
                        .topImg {                            
                            width: 100%;
                            .img {
                                display: block;
                                position: absolute;
                                top: 0;
                                left: 0%;
                                overflow: hidden;
                                #displayImage {                               
                                    width: 100%;
                                    height: 45vh;
                                    border-radius: 10px;
                                    animation: bottomLeft 450ms ease-in;
                                }
                            }
                            .row-one {
                                z-index: 2;
                                position: relative;
                                margin-top: 70%;
                                color: #969FA4;
                                p {
                                    text-align: center;
                                    margin: 2%;
                                }
                            }
                            .row-two {
                                z-index: 2;
                                position: relative;
                                #name{ 
                                    color: #FFB375;
                                    margin: 0;
                                    font-weight: lighter;
                                    text-align: center;
                                    display: none;
                                }
                                #genre { 
                                    font-weight: lighter;
                                    text-align: center;
                                    margin: 0% 0; 
                                    font-size: 25px;
                                    height: 100%;
                                    width: 100%;
                                }
                            }
                            .row-three {
                                z-index: 2;
                                position: relative;
                                display: block;
                                color: #FFB375;
                                margin: 0;
                                font-weight: lighter;
                                text-align: center;
                            }
                        }
                    }
                    
                    .row-four {
                        z-index: 2;
                        position: relative;
                        display: block;
                        .slider2 {
                            display: flex;
                            position: relative;
                            width: 100%;
                            margin: 10% 0 8%;
                            .range-input2 {
                                position:absolute;
                                width: 100%;
                                top:5%;
                                left: 0%;
                                display:flex;
                                flex-direction: column;
                            }
                            .range-input2 input {
                                -webkit-appearance:none;
                                width: 100%;
                                height:5px;
                                border-radius: 50px;
                                background:#ffffff;
                                border:none;
                                outline:none;
                            }
                            .range-input2::before {
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
                            .range-input2 input::-webkit-slider-thumb {
                                -webkit-appearance:none;
                                width:20px;
                                height:20px;
                                background:#FFB375;
                                border:none;
                                border-radius:50%;
                                cursor: pointer;
                            }
                            .range-input2 input::-webkit-slider-thumb:hover {
                                background:#FFB375;
                            }
                            .range-input2 .value {
                                color:#FFB375;
                                text-align:center;
                                font-weight:600;
                                line-height:40px;
                                height:40px;
                                overflow:hidden;
                                margin-left:10px;
                            }
                            .range-input2 .value div {
                                transition:all 300ms ease-in-out;
                            }

                        }
                        .texts {
                            display: flex;
                            position: relative;
                            width: 120%;
                            margin: 15% 0 0;
                            color: #969FA4;
                            p {
                                margin: 0;
                            }
                            #stop {
                                position: absolute;
                                right: 0;
                            }
                        }
                    }
                    .row-five {
                        z-index: 2;
                        position: relative;
                        margin: auto;
                        width: 70%;
                        .icons {
                            display: flex;
                            justify-content: center;
                            gap: 20%;
                            i {
                                width: 50%;
                                margin: 0;
                                font-size: 45px;
                            }
                            #prev {
                                text-align: left;
                            }
                            #next {
                                text-align: right;
                            }
                        }
                    }
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
                    background-color: #1ED760;
                    color: #000000;
                    width: 48%;
                    padding: 3.25% 0%;
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    i {
                        color: #000000;
                        margin-right: 2%;
                        font-size: 30px;
                        cursor: pointer;
                    }
                }
                #cancel {
                    color: #fff;
                    position: absolute;
                    right: 0%;
                }
            }
        }
    }
</style>