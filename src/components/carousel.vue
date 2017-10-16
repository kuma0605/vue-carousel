<template>
    <div>
        <div class="carouselContainer">
            <ul>
                <li class="leftContainer">
                    <div :style="leftStyle"></div>
                </li>
                <li class="leftArrow"  @click="doLeft"><i  class="fa fa-chevron-left" aria-hidden="true"></i></li>
                <li class="middleContainer">
                    <!-- <transition name="custom-classes-transition" leave-active-class="animated fadeOutRight" enter-active-class="animated fadeInLeft"> -->
                    <div :style="middleStyle" :key="middleStyle['background-image']"></div>
                    <!-- </transition> -->
                </li>
                <li class="rightArrow" @click="doRight"><i  class="fa fa-chevron-right" aria-hidden="true"></i></li>
                <li class="rightContainer">
                    <div :style="rightStyle"></div>
                </li>
            </ul>
        </div>
    </div>
</template>
<script>
    import 'font-awesome/css/font-awesome.min.css';
    import 'animate.css/animate.css';
    export default {
        props:{
            imgCategory:{
                type:Array,
                default(){
                    return [
                        {
                            path:'src/assets/banklogo10.png',
                            text:'test'
                        },
                        {
                            path:'src/assets/banklogo11.png',
                            text:'test'
                        },
                        {
                            path:'src/assets/banklogo12.png',
                            text:'test'
                        },
                        {
                            path:'src/assets/banklogo13.png',
                            text:'test'
                        },
                        {
                            path:'src/assets/banklogo14.png',
                            text:'test'
                        },
                        {
                            path:'src/assets/banklogo15.png',
                            text:'test'
                        }
                    ]
                }
            }
        },
        data(){
            return {
                leftImg:"../assets/logo.png",
                middleImg:"",
                rightImg:"src/assets/banklogo10.png",
                leftStyle:{
                    'background-image':'url()'
                },
                middleStyle:{

                },
                rightStyle:{}
            }
        },
        created(){
            //init
            this.leftStyle={
                'background-image':`url(${this.imgCategory[0].path})`
            };
            this.middleStyle={
                'background-image':`url(${this.imgCategory[1].path})`
            };
            this.rightStyle={
                'background-image':`url(${this.imgCategory[2].path})`
            };
            this.showList={
                left:0,
                middle:1,
                right:2
            };
        },
        mounted(){
            /*this.scrollCategory=setInterval(()=>{
                if(this.showList.right!==this.imgCategory.length-1){
                    this.doRight();
                }else{
                    this.showList={
                        left:0,
                        middle:1,
                        right:2
                    };
                    this.leftStyle={
                        'background-image':`url(${this.imgCategory[0].path})`
                    };
                    this.middleStyle={
                        'background-image':`url(${this.imgCategory[1].path})`
                    };
                    this.rightStyle={
                        'background-image':`url(${this.imgCategory[2].path})`
                    };
                }
            }, 5000);*/
        },
        methods:{
            doLeft(){
                
                    let showList={
                        left:this.showList.left-1,
                        middle:this.showList.middle-1,
                        right:this.showList.right-1
                    };

                    let len=this.imgCategory.length;

                    for(let key in showList){
                            let pathIndex=showList[key]>=0?showList[key]:len+showList[key];

                            this[key+'Style']={
                             'background-image':`url(${this.imgCategory[pathIndex].path})`
                            }
                            showList[key]=pathIndex;
                    };
                    this.showList=showList;
            },
            doRight(){
                    let showList={
                        left:this.showList.left+1,
                        middle:this.showList.middle+1,
                        right:this.showList.right+1
                    };

                    let len=this.imgCategory.length;

                    for(let key in showList){
                        let pathIndex=showList[key]<len?showList[key]:showList[key]-len;
                        this[key+'Style']={
                            'background-image':`url(${this.imgCategory[pathIndex].path})`
                        }
                        showList[key]=pathIndex;
                    };
                    this.showList=showList;
            }
        }
    }
</script>

<style lang="scss">
    .slide-fade-enter-active {
  transition: all .3s ease;
}
.slide-fade-leave-active {
  transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active for below version 2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
}
    .carouselContainer{
        li{
            border: 1px solid black;
            div{
                width: 100%;
                height: 100%;
                background-repeat: no-repeat;
                background-size: 100% 100%;
            }
        }
        ul{
            list-style: none;
            display: flex;
            align-items:center;
            margin:0;
            padding-left:0;
        }
        .rightContainer, .leftContainer{
            position: relative;
            width: 25%;
            height:130px;
            .layer{
                position: absolute;
                top:0;
                width: 100%;
                height: 100%;
                background: rgba(0, 0, 0, 0.3);
            }

        }
        .arrowStyle{
            text-align: center;
        }
        .leftArrow,.rightArrow{
            @extend .arrowStyle;
            width: 5%;
            cursor: pointer;
        }
        .middleContainer{
            width: 40%;
            height: 160px;
        }
    }
</style>
