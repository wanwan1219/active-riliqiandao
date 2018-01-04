
<template>
  <section>
    <div class="wh-content-all">
      <div class="wh-top-changge">
        <li @click="PreMonth">
          <div class="wh-jiantou1"></div>
        </li>
        <li class="wh-content-li">{{dateTop}}</li>
        <li @click="NextMonth">
          <div class="wh-jiantou2"></div>
        </li>
      </div>
      <div class="wh-content wh-top">
        <div class="wh-content-item" v-for="tag in textTop">{{tag}}</div>
      </div>
      <div class="wh-content">
        <div class="wh-content-item" v-for="(item,index) in list" >
          <div v-bind:class='{ 
              "wh-is-today":item.isToday,
              "wh-is-marked":item.isMarked,
              "wh-is-mark":item.isMark,
              "wh-next-day-show":(isHideOtherday&&item.nextDayShow)||item.otherMonth}'>
            {{item.id}}
          </div>
          
        </div>
      </div>
      <input type="button" v-show="!showSpan" :class='{
          "sign":needSign
          
        }' @click="markToday" value="打卡"/>
      <div v-show="showSpan" class="not-sign">打卡</div>  
      <input type="button" value="重置打卡" class="sign" @click="resetPunch"/>
    </div>
  </section>
</template>
<script>
export default {
  data() {
    return {
      textTop: ['日', '一', '二', '三', '四', '五', '六 '],
      myData: [],
      list: [],
      dateTop: '',
      needSign:true,
      notSign:false,
      showSpan:false,
    };
  },
  props: {
    markArray: { default: '[]' },
    markedArr: { default: '[]' },
    isHideOtherday: { default: false },
    allData:{default: {}}
  },
  created() {
    this.myData = new Date();
  },
  methods: {
    clickDay: function(item, index) {
      if (item.otherMonth) {
        item.otherMonth < 0 ? this.PreMonth() : this.NextMonth();
      } else {
        if (!(this.isHideOtherday && item.nextDayShow)) {
          this.$emit('choseDay', item.date);
          for (var i = 0; i < this.list.length; i++) {
            if (i == index) {
              this.list[i].isToday = true;
            } else {
              this.list[i].isToday = false;
            }
          }
        }
      }
    },
    PreMonth: function() {
      this.myData = this.getPreMonth(this.myData);
      this.$emit('changeMonth', this.dateformat(this.myData));
      this.getlist(this.myData);
      if(this.allData.data.is_punch){
        alert(1)
        let todayArr=this.dateformat(this.myData).split("/",3)
        let todayArr2=[];
        for(let i=0; i<this.markArray.length; i++){
          if(todayArr2[0]==this.markArray[i][0] && todayArr2[1]==this.markArray[i][1] && todayArr2[2]==this.markArray[i][2]){
            alert(2)
            for(let j=0 ;j<this.list.length; j++){
              if(this.list[j].date==this.dateformat(this.myData)){
                this.list[j].isMarked=true;
                this.needSign=false;
                this.notSign=true;
                this.showSpan=true;
              }
            }
          }
        } 
      }
    },
    NextMonth: function() {
      this.myData = this.getNextMonth(this.myData);
      this.$emit('changeMonth', this.dateformat(this.myData));
      this.getlist(this.myData);
      if(this.allData.data.is_punch){
        let todayArr=this.dateformat(this.myData).split("/",3)
        let todayArr2=[];
        for(let i=0; i<this.markArray.length; i++){
          if(todayArr2[0]==this.markArray[i][0] && todayArr2[1]==this.markArray[i][1] && todayArr2[2]==this.markArray[i][2]){
            for(let j=0 ;j<this.list.length; j++){
              if(this.list[j].date==this.dateformat(this.myData)){
                this.list[j].isMarked=true;
                this.needSign=false;
                this.notSign=true;
                this.showSpan=true;
              }
            }
          }
        } 
      }
    },
    /**
     * 获取上一个月
     */
    getPreMonth: function(date) {
      var timeArray = this.dateformat(date).split('/');
      var year = timeArray[0]; //获取当前日期的年份
      var month = timeArray[1]; //获取当前日期的月份
      var day = timeArray[2]; //获取当前日期的日
      var days = new Date(year, month, 0);
      days = days.getDate(); //获取当前日期中月的天数
      var year2 = year;
      var month2 = parseInt(month) - 1;
      if (month2 == 0) {
        year2 = parseInt(year2) - 1;
        month2 = 12;
      }
      var day2 = day;
      var days2 = new Date(year2, month2, 0);
      days2 = days2.getDate();
      if (day2 > days2) {
        day2 = days2;
      }
      if (month2 < 10) {
        month2 = '0' + month2;
      }
      var t2 = year2 + '/' + month2 + '/' + day2;
      return new Date(t2);
    },
    /**
     * 获取下一个月
     */
    getNextMonth: function(date) {
      var arr = this.dateformat(date).split('/');
      var year = arr[0]; //获取当前日期的年份
      var month = arr[1]; //获取当前日期的月份
      var day = arr[2]; //获取当前日期的日
      var days = new Date(year, month, 0);
      days = days.getDate(); //获取当前日期中的月的天数
      var year2 = year;
      var month2 = parseInt(month) + 1;
      if (month2 == 13) {
        year2 = parseInt(year2) + 1;
        month2 = 1;
      }
      var day2 = day;
      var days2 = new Date(year2, month2, 0);
      days2 = days2.getDate();
      if (day2 > days2) {
        day2 = days2;
      }
      if (month2 < 10) {
        month2 = '0' + month2;
      }

      var t2 = year2 + '/' + month2 + '/' + day2;
      return new Date(t2);
    },
    getDaysInOneMonth: function(date) {
      //通过获取下月面0号的日期可以知道这个月有多少天
      var getyear = date.getFullYear();
      var getmonth = date.getMonth() + 1;
      getmonth = parseInt(getmonth, 10);
      var d = new Date(getyear, getmonth, 0);
      return d.getDate();
    },
    getMonthweek: function(date) {
      //获取本月第一天是星期几，然后在去向前空几个
      var getyear = date.getFullYear();
      var getmonth = date.getMonth() + 1;
      var dateOne = new Date(getyear + '/' + getmonth + '/1');//星期日返回0 
      return dateOne.getDay() == 0 ? 0 : dateOne.getDay() ;
    },
    getlist: function(date) {
      //渲染出来当前list
      var mygetMonth = date.getMonth() + 1 < 10 ? '0' + (date.getMonth() + 1) : date.getMonth() + 1;
      this.dateTop = date.getFullYear() + '年' + mygetMonth + '月';
      var array = [];
      
      for (var i = 0; i < this.getDaysInOneMonth(date); i++) {
        let sameData = [date.getFullYear() , mygetMonth , i+1];
        
        if (
          this.dateformat(new Date()) ==
          this.dateformat(new Date(date.getFullYear() + '/' + (date.getMonth() + 1) + '/' + (i + 1)))
        ) {
          array = array.concat({
            //如果当前这天是今天 isToday是true
            id: i + 1,
            date: date.getFullYear() + '/' + (date.getMonth() + 1) + '/' + (i + 1),
            isToday: true,
            isMark: this.hasSameArray(this.markArray , sameData),
            isMarked: this.hasSameArray(this.markedArr , sameData),
            nextDayShow:
              new Date(date.getFullYear() + '/' + (date.getMonth() + 1) + '/' + (i + 1)).getTime() -
                new Date().getTime() >
              0
          });
          this.$emit(
            'isToday',
            this.dateformat(new Date(date.getFullYear() + '/' + (date.getMonth() + 1) + '/' + (i + 1)))
          );
        } else {
          array = array.concat({
            id: i + 1,
            date: date.getFullYear() + '/' + (date.getMonth() + 1) + '/' + (i + 1),
            isToday: false,
            isMark: this.hasSameArray(this.markArray , sameData),
            isMarked: this.hasSameArray(this.markedArr , sameData),
            nextDayShow:
              new Date(date.getFullYear() + '/' + (date.getMonth() + 1) + '/' + (i + 1)).getTime() -
                new Date().getTime() >
              0
          });
        }
      }
      var array2 = [];
      var num = this.getDaysInOneMonth(this.getPreMonth(date)) - this.getMonthweek(date) + 1;
      for (var i = 0; i < this.getMonthweek(date); i++) {
        array2 = array2.concat({ otherMonth: -1, id: num + i });
      }
      array = array2.concat(array);
      var length = 7 - array.length % 7;
      if (length < 7) {
        for (let i = 0; i < length; i++) {
          array.push({ otherMonth: 1, id: i + 1 });
        }
      }
      this.list = array;
    },
    dateformat: function(date) {
      return date.getFullYear() + '/' + (date.getMonth() + 1) + '/' + date.getDate();
    },
    hasSameArray(arr1 , arr2) {
      let isSame = false;
      //console.log(arr1 , arr2)
      for (var i = 0; i < arr1.length; i++) {
          if(arr1[i][0] == arr2[0]&&arr1[i][1] == arr2[1]&&arr1[i][2] == arr2[2]){
            isSame = true;
          }
       }
      return isSame
    },
    markToday(){
      if(this.allData.data.is_punch){
        // alert("今天已经签到了")
        for(let j=0 ;j<this.list.length; j++){
          if(this.list[j].date==this.dateformat(this.myData)){
            //签到成功
            this.list[j].isMarked=true;
            this.needSign=false;
            this.notSign=true;
            this.showSpan=true;
          }
        }
      }else{
        //今天没签到
        // let todayArr=this.dateformat(this.myData).split("/",3)
        // let todayArr2=[];
        // for(let i=0;i<todayArr.length;i++){
        //   todayArr2.push(Number(todayArr[i]));
        // }
        // for(let i=0; i<this.markArray.length; i++){
        //   if(todayArr2[0]==this.markArray[i][0] && todayArr2[1]==this.markArray[i][1] && todayArr2[2]==this.markArray[i][2]){
            //判断今天是否在活动日期里 在的话点击按钮加isMarked
            for(let j=0 ;j<this.list.length; j++){
              if(this.list[j].date==this.dateformat(this.myData)){
                //签到成功
                this.list[j].isMarked=true;
                this.needSign=false;
                this.notSign=true;
                this.showSpan=true;
              }
            }
          // }else{
            //不能签到
            
          // }
          this.postPunch()
        // }
      }
      
      
    },
    postPunch(){
      let cId = this.$route.params.courseId? this.$route.params.courseId: this.$route.params.id;
      this.$axios.$post(`/activity/chant-punch-card/${cId}/punch`)
      // .then((res)=> {
      //   if(res.data.code == -1 ) {
      //     // this.markToday()
      //   }
      // })
    },
    resetPunch(){
      this.$axios.$get("/activity/chant-punch-card/reset",{course_id: this.$route.params.courseId? this.$routze.params.courseId: this.$route.params.id}).then(res=>{
        // if(res.data.code=0){
        //   this.needSign=true;
        //   this.notSign=false;
        //   this.showSpan=false;
        //   this.list[j].isMarked=false;
        // }
      })
    }
  },
  mounted() {
    this.getlist(this.myData);
    // this.markToday()
    if(this.allData.data.is_punch){
      for(let j=0 ;j<this.list.length; j++){
        if(this.list[j].date==this.dateformat(this.myData)){
          //签到成功
          this.list[j].isMarked=true;
          this.needSign=false;
          this.notSign=true;
          this.showSpan=true;
        }
      }
    }
  },
  watch: {
    markArray(val, oldVal) {
      var list = this.list;
      for (var i = 0; i < list.length; i++) {
        list[i].isMark = false;
        if (list[i].date) {
          for (var n = 0; n < val.length; n++) {
            if (list[i].id == val[n]) {
              list[i].isMark = true;
            }
          }
        }
      }
      this.list = list;
    }
  },
  
};
</script>
<style scoped>
* {
  margin: 0;
  padding: 0;
}

.wh-content-all {
  background-color: white;
  width: 355px;
  overflow: hidden;
  padding-bottom: 8px;
  color: black;
  background: #FFFFFF;
  box-shadow: 0 2px 8px 0 #D8D8D8;
  border-radius: 40px;
  margin: 0 10px;
}
.wh-content {
  display: flex;
  flex-wrap: wrap;
  width: 355px;
  overflow: hidden;
}

.wh-content:first-child .wh-content-item {
  color: #ddd;
  font-size: 16px;
  height: 15vw;
  line-height: 15vw;
}

.wh-content-item {
  font-size: 15px;
  height: 30px;
  line-height: 30px;
  width: 30px;
  margin: 10px;
  text-align: center;
  color: black;
}


.wh-is-mark {
  width: 100%;
  height: 100%;
  line-height: 30px;
  background: #F5F5F5;
  border-radius: 20px;
  z-index: 2;
}

.wh-is-today {
  width: 100%;
  height: 100%;
  line-height: 30px;
  text-align: center;
}

.wh-top-changge {
  display: flex;
  color: black
}

.wh-top-changge li {
  display: flex;
  color: black;
  font-size: 18px;
  flex: 1;
  justify-content: center;
  align-items: center;
  height: 47px;
}

.wh-top-changge .wh-content-li {
  flex: 1;
  font-family: PingFangSC-Regular;
  font-size: 18px;
  color: #333333;
  letter-spacing: 0.15px;
}

.wh-jiantou1 {
  width: 11px;
  height: 11px;
  border-top: 2px solid #A4AAB3;
  border-left: 2px solid #A4AAB3;;
  transform: rotate(-45deg);
}

.wh-jiantou2 {
  width: 11px;
  height: 11px;
  border-top: 2px solid #A4AAB3;
  border-right: 2px solid #A4AAB3;
  transform: rotate(45deg);
}
.wh-next-day-show {
  color: #bfbfbf;
}
.wh-is-marked {
  font-family: PingFangSC-Regular;
  font-size: 14px;
  color: #FFFFFF;
  letter-spacing: 0.12px;
  background: #54C7FC;
  border: 2px solid #FFFFFF;
}

.wh-top{
  font-family: PingFangSC-Regular;
  font-size: 18px;
  color: #333333;
  letter-spacing: 0.15px;
}
.sign{
  width: 230px;
  height: 44px;
  background:#54C7FC;
  border-radius: 22px;
  color: white;
  outline: none;
  border: none;
  margin-left: 63px;
}
.not-sign{
  width: 230px;
  height: 44px;
  background:#ccc;
  border-radius: 22px;
  color: white;
  outline: none;
  border: none;
  margin-left: 63px;
  text-align: center;
  line-height: 44px;
  cursor: pointer;
}
</style>