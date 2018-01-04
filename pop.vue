<template>
    <div>
        <div class="pop-con" v-if="showPop">
            <div class="img-wrap">
                <img class="con-img" src="../../static/images/active_sign/pop_img.png" alt="">
                <nuxt-link to="/active/active"></nuxt-link>
                <img @click="closePop" class="con-close" src="../../static/images/active_sign/pop_close.png" alt="">
            </div>
            
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            showPop:true
        }
    },
    created(){
        // this.$nextTick(()=>{

        // })
    },
    methods:{
        closePop(){
            this.showPop=false;
        },
    },
    
}
</script>

<style>
    .pop-con{
        width: 100%;
        height: 100%;
        position: fixed;
        overflow: hidden;
        top: 0;
        left: 0;
        z-index: 999;
        background: rgba(0,0,0,.8);
        text-align: center;
        /* overflow: hidden; */
    }  
    .pop-con .img-wrap a{
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate3d(-50%,-50%,0); 
        width: 500px;
        height: 500px;
        display: inline-block;
    }
    .pop-con .con-img{
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate3d(-50%,-50%,0);
        width: 500px;
        height: 500px;
    }
    .pop-con .con-close{
        position: absolute;
        top:50%;
        margin-top: 300px;
        /* width: 45px;
        height: 45px; */
        transform: translate3d(-50%,-50%,0); 
    }
</style>