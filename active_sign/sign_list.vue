<template>
<div class="sign-bottom clear-fix">
    <div class="sign-left">
        <img src="../../static/images/active_sign/signimg.png" alt="">
    </div>
    <div class="sign-right" @click="showSign">
        <div class="sign-img">
            <img src="../../static/images/active_sign/sign.svg" alt="">
        </div>
        <div class="sign-info">
            <p class="firp">打卡</p>
            <p class="sedp">{{msg}}</p>
        </div>
    </div>
    <signInner v-show="showsigninner" :sign="showsigninner" @signHide="changeSign"></signInner>
</div>
</template>

<script>
import signInner from "@/components/active_sign/sign_inner"
export default {
data(){
    return{
        showsigninner:false,
        msg:"第一天"
    }
},
components:{
    signInner
},
methods:{
    showSign(){
        this.showsigninner=true;
        document.body.setAttribute("style", "overflow:hidden")
        // this.$emit("getsign",this.showsigninner)
    },
    changeSign(val){
        this.showsigninner=val
    }
}
}
</script>

<style>
    
    .sign-bottom{
        position: fixed;
        left: 0;
        bottom: 0;
        width: 100%;
        height: 60px;
        background: #FFFFFF;
        box-shadow: 0 -2px 8px 0 #D8D8D8;
    }
    .sign-bottom .sign-left{
        height: 100%;
        float: left;
    }
    .sign-bottom .sign-left img{
        width: 565px;
        position: absolute;
        left: 50%;
        transform: translate3d(-60%,-50%,0);
        top: 50%;
    }
    .sign-bottom .sign-right{
       background: #54C7FC;
       color: white;
       float: right;
       width: 129px;
       height: 100%;
       cursor: pointer;
    }
    .sign-right .sign-img{
        width: 44px;
        height: 36px;
        float: left;
        margin: 9px 12px 12px 18px;
    }
    .sign-right .sign-info{
        float: left;
    }
    .sign-right .sign-info .firp{
        color: #FFFFFF;
        font:500 18px/30px "PingFangSC-Regular"
    }
    .sign-right .sign-info .sedp{
        font-family: PingFangSC-Regular;
        font-size: 12px;
        color: #FFFFFF;
        line-height: 25px;
    }
</style>
