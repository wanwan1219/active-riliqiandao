<template>
  <div :class="{'layer':layer}" v-if="ready">
    <div class="content" >
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
    <Calendar 
              v-on:choseDay="clickday"
              v-on:isToday="clicktoday"
              v-on:changeMonth="changeDate"
              :markArray="markArr"
              :markedArr="makedArr"
              :isHideOtherday=false
              :allData="allData"
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
      markArr: [],
      makedArr: [],
      cumulSign: "",
      cumulTime: "",
      cumulBeat: "",
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
      ready:false,
      result:[],
      allData:""
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
      // console.log(this.layer)
      if(window.innerWidth){
        this.layer.width = window.innerWidth+'px';
      }else if((document.body) && (document.body.clientWidth)){
        this.layer.width = document.body.clientWidth+'px';
      }
      // console.log(this.layer)
      if (window.innerHeight)
        this.layer.height = window.innerHeight+'px';
      else if ((document.body) && (document.body.clientHeight))
        this.layer.height =document.body.clientHeight+'px';
    },
    getDate(){
      //调取后台数据 活动日期 放到数据池 
      let arr=[];
      for(let i=0;i<this.result.length;i++){
        let datetime=this.result[i].date.split("-")
        for(let j=0;j<datetime.length;j++){
          datetime[j] = Number(datetime[j])
        }
        arr.push(datetime); 
      }
      this.markArr =  arr;
      this.ready = true;
    },
    getMarkedData(){
      //获取被标记的日期 
      let arr=[];
      //console.log(this.result)
      for(let i=0;i<this.result.length;i++){
        if(this.result[i].punch==true){
          var markedDate=this.result[i].date.split("-");  
          for(let j=0;j<markedDate.length;j++){
            markedDate[j] = Number(markedDate[j])
          }
        }else{
          markedDate=[];
        }
      }
      //console.log(markedDate)
      this.makedArr.push(markedDate)
    },
    getResult(){
      this.$axios.$get("/activity/chant-punch-card").then(data => {
        if(data.data.code==0){
          this.allData=data.data;
          this.result=data.data.data.punch_record;
          this.cumulSign=data.data.data.sign_in_num;
          this.cumulBeat=data.data.data.beat_other;
          this.cumulTime=data.data.data.study_time;
          this.$nextTick(()=>{
            this.getDate()
            this.getMarkedData()
          })
        }
      }).catch(()=>{

      })
    }
  },
  created(){
    this.getResult()
    
  },
  mounted() {
    this.getwin()
      
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
