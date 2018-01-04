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
    <signInner v-if="showsigninner" :sign="showsigninner" @signHide="changeSign" ></signInner>
</div>
</template>

<script>
import signInner from "@/components/active_sign/sign_inner"
export default {
props: ['day','isMin'],
data(){
    return{
        showsigninner:false,
        msg:"",
    }
},

components:{
    signInner
},

mounted(){
    this.getmsg();
    // this.resetPunch()
},
methods:{
    showSign(){

        if(this.userInfo.user_id && this.isMin.is_mine){
            this.showsigninner=true;
            document.body.setAttribute("style", "overflow:hidden")
        }else if(!this.userInfo.user_id){
            this.$messageBox({
                info:{
                    name:'提示',
                    content:"请登录",
                    cancel:function() {

                    },
                    confirm: () => {
                        console.log('/login?redirect_url='+window.location.href);
                        window.location.href = '/login?redirect_url='+window.location.href;
                    }
                }
            })
        }else if(this.userInfo.user_id && !this.isMin.is_mine){
            this.$tooltips.error("请购买");
        }
        
    },
    changeSign(val){
        this.showsigninner=val
    },
    getmsg(){
        let arr=["一","二","三","四","五","六","七","八","九","十"]
        this.msg="第"+arr[(this.day)-1]+"天";
    },
    
},
computed:{
    userInfo() {
        return this.$store.state.userInfo;
    }
},
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
        z-index: 999;
    }
    .sign-bottom .sign-left{
        height: 100%;
        float: left;
        text-align: center;
        width: 77%;
    }
    .sign-bottom .sign-left img{
        width: 565px;
        margin-top: 20px;
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
