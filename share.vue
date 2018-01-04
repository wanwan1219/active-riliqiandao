<template>
    <div class="share" >
        <share :config="config" class="fl"></share>
    </div>
</template>

<script>
if (process.browser) {
    require('~/plugins/share.js');
}
export default {
    data(){
        return{
            msg:"分享",
            config:{
                sites: ['qzone', 'qq', 'weibo','wechat', 'douban'],
                title: "学国学网",
                image: "http://b.hiphotos.baidu.com/image/h%3D300/sign=0dc79257c2ef7609230b9f9f1edca301/6d81800a19d8bc3eb00690008b8ba61ea9d345e9.jpg",
                url: `www.xueguoxue.com`
            }
        }
    }
}
</script>

<style lang="scss">
@import "~static/course/share.min.css";
</style>