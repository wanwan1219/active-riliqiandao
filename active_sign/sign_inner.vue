<template>
  <div :class="{'layer':layer}">
    <div class="content">
    <div class="close" @click="closeSign"><img src="../../static/images/active_sign/close.svg" alt=""></div>
    <div class="sign-count">
      <div class="cumul cumul-sign">
        <p class="cumul-top">累计签到</p>
        <p class="cumul-num">{{cumulSign}} <span>天</span></p>
      </div>
      <div class="cumul cumul-time">
        <p class="cumul-top">累计时长</p>
        <p class="cumul-num">{{cumulTime}} <span>min</span></p>
      </div>
      <div class="cumul cumul-beat">
        <p class="cumul-top">已打败</p>
        <p class="cumul-num">{{cumulBeat}}%</p>
      </div>
    </div>
    <Calendar v-on:choseDay="clickday"
              v-on:isToday="clicktoday"
              v-on:changeMonth="changeDate"
              :markArray="markArr"
              :markedArr="makedArr"
              :isHideOtherday=false
    ></Calendar>
    <div @mouseover="show" @mouseout="hide"><div class="sharemsg">{{msg}}</div>
        <share v-show="showShare"></share>
    </div>
  </div>
  </div>
</template>
<script>
import Calendar from "@/components/active_sign/calender";
import share from "@/components/active_sign/share";

export default {
  components: { Calendar, share },
  props:{sign: { default: true },},
  data() {
    return {
      markArr: [
        [2017, 12, 24],
        [2017, 12, 25],
        [2017, 12, 26],
        [2017, 12, 27],
        [2017, 12, 28],
        [2017, 12, 29],
        [2017, 12, 30]
      ],
      makedArr: [[2017, 12, 24], [2017, 12, 25]],
      cumulSign: 10,
      cumulTime: 50,
      cumulBeat: 90,
      msg: "分享",
      showShare: false,
      WinWidth:0,
      WinHeight:0,
      layer:{
        width: "",
        height: "",
        background: "rgba(0,0,0,0.8)",
        position: "absolute",
        zIndex: 999,
        top: 0,
        left: 0
      },
    }
  },
  methods: {
    clickday(data) {},
    clicktoday(data) {
      // console.log(data); //跳到了本月
    },
    changeDate(data) {
      // Toast("切换到的月份为" + data, 2000);
      // console.log(data); //左右点击切换月份s
    },
    markToday() {},
    show() {
      this.showShare = true;
    },
    hide() {
      this.showShare = false;
    },
    closeSign(){  
        this.sign=false;
        // console.log(this.sign)
        this.$emit("signHide",this.sign);
        document.body.setAttribute("style", "overflow:");
    },
    getwin(){
      console.log(this.layer)
      if(window.innerWidth){
        this.layer.width = window.innerWidth+'px';
      }else if((document.body) && (document.body.clientWidth)){
        this.layer.width = document.body.clientWidth+'px';
      }
      console.log(this.layer)
      if (window.innerHeight)
        this.layer.height = window.innerHeight+'px';
      else if ((document.body) && (document.body.clientHeight))
        this.layer.height =document.body.clientHeight+'px';
    }
  },
  mounted() {
    //调取后台数据 放到数据池
    this.getwin()
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.layer {
  background: rgba(0,0,0,0.8);
   position: fixed;
   z-index: 999;
   top: 0;
   left: 0;
   width: 100%;
   height: 100%;
}
.content {
    width: 375px;
    background: #fff;
    border-radius: 8px;
    position: absolute;
    margin: auto;
    top: 50%;
    left: 50%;
    transform: translate3d(-50%,-50%,0);
}
.sign-count {
  display: flex;
  width: 375px;
}
.close img{
  width: 18px;
  height: 26px;
  
}
.sign-count > div {
  flex: 1;
  text-align: center;
  border-left: 1px dotted #d8d8d8;
  margin-top: 30px;
  margin-bottom: 20px;
}
.sign-count > div:first-of-type {
  border-left: none;
}
.cumul-top {
  font-family: PingFangSC-Regular;
  font-size: 14px;
  color: #666666;
  letter-spacing: 0.14px;
  line-height: 30px;
}
.cumul-num {
  font-family: PingFangSC-Medium;
  font-size: 24px;
  color: #333333;
  letter-spacing: 0.14px;
}
.cumul-num span {
  font-family: PingFangSC-Regular;
  font-size: 14px;
  color: #333333;
  letter-spacing: 0.14px;
}
.sharemsg {
  cursor: pointer;
  text-align: center;
  line-height: 60px;
  font-family: PingFangSC-Regular;
  font-size: 14px;
  color: #54C7FC;
  letter-spacing: 0.12px;
}
.share {
  position: absolute;
  cursor: pointer;
  bottom: 18px;
  left: 55%;
}
.close{
    color: #444546;
    position: absolute;
    width: 30px;
    height: 30px;
    background: #FFFFFF;
    box-shadow: 2px 4px 8px 0 rgba(0,0,0,0.10);
    border-radius: 50%;
    right: 0;
    top: 0;
    margin-top: -15px;
    margin-right: -15px;
}
</style>
