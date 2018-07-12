<template>
    <div class="banner-box"
         @mouseover="stop"
         @mouseleave="autoShow"
    >
        <div ref="bannerContent" class="banner-content">
            <transition-group
                    name="slide"
                    :css="false"
                    @before-enter="beforeEnter"
                    @enter="enter"
                    @leave="leave"
            >
                <div ref="slideBar"
                     class="slide-bar"
                     v-for="(item, index) in images"
                     :key="index"
                     v-show="index === currentIndex">
                    <a href="#">
                        <img ref="img" :src="item.src">
                    </a>
                </div>
            </transition-group>
            <div @click="prevShow" class="control prev"><a href="#"><i class="iconfont icon-back"></i></a></div>
            <div @click="nextShow" class="control next"><a href="#"><i class="iconfont icon-more"></i></a></div>
            <div ref="bannerDots" class="banner-dots">
        <span class="dot"
              v-for="(dot, index) in dots"
              :key="index"
              ref="dot"
              :class="{currentDot : index ===currentIndex }"
        >
        </span>
            </div>
        </div>
    </div>
</template>

<script>
    import Velocity from 'velocity-animate'
    const SLIDE_MODE = 0
    /* const OPACITY_MODE = 1 */
    export default {
        data () {
            return {
                currentIndex: 0,
                timer: null
            }
        },
        props: {
            images: {
                type: Array,
                default: () => []
            },
            loop: {
                type: Boolean,
                default: true
            },
            speed: {
                type: Number,
                default: 2000
            },
            autoplay: {
                type: Boolean,
                default: true
            },
            model: {
                type: Number,
                default: SLIDE_MODE
            }
        },
        mounted () {
            this.$nextTick(() => {
                this.setImage()
                if (this.autoplay) {
                    this.autoShow()
                }
                window.addEventListener('resize', () => {
                    this.setImage()
                })
            })
        },
        computed: {
            dots () {
                return this.images.length
            }
        },
        methods: {
            setImage () {
                let me = this
                this.$refs.img.forEach((item) => {
                    item.style.width = window.innerWidth * 0.7 + 'px'
                    item.style.height = me.$refs.bannerContent.clientHeight + 'px'
                    item.style.zIndex = 5
                })
            },
            nextShow () {
                if (this.loop) {
                    if (this.currentIndex === 4) {
                        this.currentIndex = 0
                    } else {
                        this.currentIndex = this.currentIndex + 1
                    }
                } else {
                    if (this.currentIndex === 4) {
                        this.currentIndex = 4
                    } else {
                        this.currentIndex = this.currentIndex + 1
                    }
                }
            },
            prevShow () {
                if (this.loop) {
                    if (this.currentIndex === 0) {
                        this.currentIndex = 4
                    } else {
                        this.currentIndex = this.currentIndex - 1
                    }
                } else {
                    if (this.currentIndex === 0) {
                        this.currentIndex = 0
                    } else {
                        this.currentIndex = this.currentIndex - 1
                    }
                }
            },
            autoShow () {
                this.timer = setInterval(this.nextShow, this.speed)
            },
            beforeEnter (el) {
                el.style.opacity = 0
                el.style.zIndex = 5
            },
            enter (el, done) {
                Velocity(
                    el,
                    { opacity: 1, zIndex: 10 },
                    { duration: 1000,
                        easing: [ 0.4, 0.01, 0.165, 0.99 ],
                        complete: done }
                )
            },
            leave (el, done) {
                Velocity(
                    el,
                    { opacity: 0, zIndex: 5 },
                    { duration: 1000,
                        easing: [ 0.4, 0.01, 0.165, 0.99 ],
                        complete: done }
                )
            },
            stop () {
                clearInterval(this.timer)
            }
        },
        watch: {
            currentIndex (newIndex) {
            }
        }
    }
</script>

<style scoped>
    .banner-box {
        height: 100%;
    }
    .banner-content{
        position: relative;
        width: 100%;
        height:100%;
    }
    .slide-bar {
        position: absolute;
        top: 0;
        bottom: 0;
        left: 0;
    }

    .control {
        position: absolute;
        top: 50%;
        height: 50px;
        width: 50px;
    }

    .banner-content .prev, .next {
        z-index: 15;
        height: 40px;
        line-height: 40px;
        text-shadow: 0 2px 4px rgba(7, 17, 27, .6);
        border-radius: 2rem;
    }
    .banner-content .prev:hover, .next:hover{
        color: #fff;
        background: rgba(7,17,27,.6);
    }
    .banner-content .icon-more,.icon-back{
        font-size: 50px;
        color: #e20f0b;
    }
    .next {
        right: 0;
    }
    .prev {
        left: 0;
    }
    .banner-dots {
        position: absolute;
        bottom: 0;
        left: 25%;
        display: flex;
        justify-content: space-between;
        width: 40%;
        height: 15px;
        padding: 5px;
    }
    .dot {
        z-index: 15;
        display: inline-block;
        width: 8px;
        height: 8px;
        border-radius: 50%;
        margin-left: 8px;
        background: rgba(7,17,27,.8);
        border: 1px solid rgba(255,255,255,.6);
        transition: transform .2s;
        cursor: pointer;
    }
    .currentDot {
        background: #eee;
    }
</style>
