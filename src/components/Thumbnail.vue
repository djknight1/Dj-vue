<template>
    <div class="wrapper">
        <h2 class="thumbnail-title">我的作品</h2>
        <span class="sub-title">Life ain't nothing but struggle</span>
        <div class="thumbnails">
            <div
                    class="thumbnail-item"
                    v-for="(item, index) in thumbnails"
                    :key="index"
            >
                <div>

                    <img :src="item.src" >
                    <p class="title1"><strong>{{item.name}}</strong></p>
                    <p class="title2">{{item.desc}}</p>
                    <p class="learn-more">learn more ></p>

                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default{
        props: {
            thumbnails: {
                type: Array,
                default: () => []
            }
        }
    }
</script>

<style scoped>
    .thumbnail-title{
        margin-bottom:15px;
    }
    .sub-title {
        font-size: 1rem;
        color: #999;
        display: block;
        text-align: center;
    }
    .thumbnails {
        width: 80%;
        margin:1.7rem auto;
        display: flex;
        padding-top:50px;
        justify-content: space-around;
    }
    .thumbnail-item{
        flex-basis: 20%;
        height: 15rem;
        margin-right: 4rem;
        box-shadow: 0 1px 1px 1px rgba(0, 0, 0, 0.12);
        box-sizing: border-box;
        background: #fff;
        border-radius: 2px;
        display: inline-block;
        position: relative;
        padding: 0 6px;
        text-align: center;
        cursor: pointer;
        -webkit-transition: .1s ease;
        -moz-transition: .1s ease;
        -ms-transition: .1s ease;
        -o-transition: .1s ease;
        transition: .1s ease;
    }
    .thumbnail-item:hover{
        box-shadow: 0 1px 1px 2px rgba(0, 0, 0, 0.12);
        -webkit-transform: translate3d(0, -3px, 0);
        -moz-transform:translate3d(0, -3px, 0);
        -ms-transform: translate3d(0, -3px, 0);
        -o-transform:translate3d(0, -3px, 0);
        transform: translate3d(0, -3px, 0);
    }
    .thumbnail-item img {
        display: block;
        margin:-3.5rem auto 0 auto;
        height: 4rem;
        width: 4rem;
        max-width:100%;
        border:0;
    }
    .thumbnail-item .title1{
        color: rgba(0, 0, 0, 0.87);
        margin-top: 8px;
        margin-bottom: 8px;
        font-size: 1.4rem;
    }
    .thumbnail-item .title2 {
        font-size: 1.4rem;
        color: rgba(0, 0, 0, 0.56) !important;
    }
    .learn-more {
        font-size: 1.2rem;
        color: #C2A661;
        font-weight: 400;
        opacity: 0.7;
        text-transform: none;
    }
</style>
