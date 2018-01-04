<template>
    <div class="suspend">
        <div class="online">
            <img src="../../static/images/active_sign/online_consulting.svg" alt="">
            <p>在线咨询</p>
        </div>
        <div :class='{"qr":qrOld,"qrhover":qrIsShow}' @mouseover="showqr" @mouseout="hideqr" >
            <div class="dotted"></div>
            <img src="../../static/images/active_sign/qr_code.svg" alt="">
            <p>关注我们</p>
            <div class="dotted"></div>            
            <div v-show="qrIsShow" class="bigqr">
                <img src="../../static/images/active_sign/qr.png" alt="">
                <p>扫码关注</p>
            </div>
        </div>
        <div class="to-top" @click="toTop">
            <img src="../../static/images/active_sign/to_top.svg" alt="">
            <p>返回顶部</p>
        </div>
    </div>
</template>

<script>
export default {
    data(){
       return{
            qrIsShow:false,
            qrOld:true,
       }
    },
    methods:{
        showqr(){
            this.qrIsShow=true;
            // alert(1)  
        },
        hideqr(){
            this.qrIsShow=false;
        },
        toTop(){
            document.documentElement.scrollTop = document.body.scrollTop =0
        }
    }
}
</script>

<style scoped>
    .suspend{
        width: 64px;
        height: 205px;
        background: #3094C5;
        box-shadow: 0 0 2px 0 #54C7FC;
        border-radius: 8px; 
        position: fixed;
        right: 20px;
        bottom: 90px;
        display: flex;
        flex-direction: column;
        font-family: PingFangSC-Regular;
        font-size: 12px;
        color: #FFFFFF;
    }
    .suspend > div{
        flex: 1; 
        box-sizing: border-box;
    }
    .dotted{
        border-bottom: 2px dotted #fff;  
        margin: 0 10px;
    }
    .suspend > div img{
        width: 25px;
        height: 20px;
        display: block;
        margin:10px auto 0;
    }
    .suspend > div p{
        text-align: center;
        margin-top:5px;
    }
    .suspend .qr img{
        width: 25px;
        height: 25px;
        display: block;
    }
    .suspend .qr p{
        margin-bottom: 13px;
    }
    .bigqr{
        position: absolute;
        left: -123px;
        top: -12px;
        width: 123px;
        height: 152px;
        background: #0F5D83;
        border-radius: 4px 4px 0 0;
    }
    .suspend .qr .bigqr img{
        width: 113px;
        height: 113px;
    }
    .suspend .qr .bigqr p{
        text-align: center;
        font-family: PingFangSC-Regular;
        font-size: 12px;
        color: #FFFFFF;
    }
    .suspend .qrhover{
        background: #0F5D83;
    }
    
</style>
