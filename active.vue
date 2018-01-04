<template>
    <div class="active-wrap">
        <div class="active-top">
            <div class="inner">
                <img src="../../static/images/active_sign/title.png" alt="">
                <img class="prompt" src="../../static/images/active_sign/prompt.png" alt="">
            </div>
        </div>
        <img class="active-air" src="../../static/images/active_sign/active_time.png" alt="">
        <div class="active-con">
            <div class="top-cloud"></div>
            <div class="inner">
                <div class="active-content">
                    <p>1.诵读国学经典，积淀文化底蕴</p>
                    <p>2.引起学生兴趣，趣味中学习经典</p>
                    <p>3.打破课堂限制，给予学生与名师学习机会</p>
                </div>
                <div class="active-img">
                    <p>2018年1月20日至1月26日</p>
                    <img class="time-img" src="../../static/images/active_sign/time.png" alt=""></br>
                    <img src="../../static/images/active_sign/join.png" alt="">
                    <p>亲子诵读、视频跟读、亲子对读</p>
                    <img src="../../static/images/active_sign/rule.png" alt="">
                    <p class="text-lt">（1）方式一：用户点击【学国学网】公众号底部菜单栏【传诵经典】，进入“传诵经典， 国学‘声声’不息”活动页；</p>
                    <p class="text-lt">（2）方式二：登录学国学网www.xueguoxue.com，从“传诵经典， 国学‘声声’不息”活动弹窗或导航活动进入活动页；</p>
                    <p class="text-lt">（3）进入活动页点击12门任意课程，即可打卡；</p>
                    <p class="text-lt">（4）打卡为连续7天，2018年1月20日~1月26日。</p>
                    <img src="../../static/images/active_sign/reword.png" alt="">
                    <p class="text-lt">（1）打卡期间，坚持7天连续打卡，即为完成传诵经典活动，将在活动结束后为您的账号
                    返300夫子币（1夫子币=1元），中断一天不返夫子币。</p>
                    <p class="text-lt">（2）打卡成功后，分享到朋友圈集赞满50个，截图发送到学国学网公众号，即可领取
                    100夫子币。若连续7天集满则获得700夫子币哦！</p>
                    <p class="text-lt">温馨提示：夫子币为学国学网专用币，可在学国学网购换任何课程， 不可提现。(活动最终解释权归学国学网所有)</p></br></br>
                </div>  
            </div>
            <div class="course-wrap">
                <div class="right-lines"></div>
                <div class="inner">
                    <div class="course-con">
                        <div v-for="(item, index) in courseArr" class="course" :class='{"cloud":index==isActive}' @click="showCloud(index)">
                            <nuxt-link :to="item" target="_blank"></nuxt-link>
                        </div>
                    </div>
                </div>
                <div class="sun"></div>
                <div class="bot-cloud"></div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            course:true,
            cloud:false,
            isActive:0,
            courseArr:["/course/1186","/course/1182","/course/1184","/course/483","/course/397","/course/417","/course/519","/course/553","/course/135","/course/1266","/course/1267","/course/1286"]
        }
    },
    created(){
        this.$nextTick(()=>{
            this.showCloud(0)
        })
    },
    methods:{
        showCloud(index){
            this.isActive = index ||0;
            // let allCourse=this.$el.getElementsByClassName("course");
            // for(let i=0;i<allCourse.length;i++){
            //     allCourse[i].className="course";
            // }
            // allCourse[index].className="course cloud"
        }
    }
}
</script>

<style scoped>
    @media (min-width: 1200px){
        .inner{
            width: 1200px;
            margin: auto;
        }
        .active-wrap{
            position: relative;
        }
        .active-top{
            background: url("../../static/images/active_sign/head_dark_lines.png") no-repeat center top,url("../../static/images/active_sign/connect.png") no-repeat center bottom #0168CF;
            width: 100%;
            height: 1310px;
            text-align: center;
            background-size: 100%;
        }
        .active-top .prompt{
            width: 620px;
            height: 84px;
        }
        .active-wrap .active-air{
            position: absolute;
            top:500px;
            left: 50%;
            top: 1075px;
            transform: translate3d(-50%,-50%,0)
        }
        .active-con{
            width: 100%;
            text-align: center;
            /* position: absolute;
            top: 700px; */
            padding-top: 230px;
            background:  #001278;
        }
        .active-con .top-cloud{
            width: 23.6%;
            height: 316px;
            background: url("../../static/images/active_sign/top_cloud.png") no-repeat center left;
            background-size: 100%;
            position: absolute;
            left: 0;
            top:2000px;
            z-index: 3;
        }
        .active-con .active-content{
            width: 490px;
            height: 105px;
            position: absolute;
            left: 50%;
            margin-left: -245px;
            top:1100px;
            margin-top: -50px;
            font-family: PingFangSC-Medium;
            font-size: 24px;
            color: #EDECD3;
            line-height: 35px;
            text-align: left;
        }
        .active-con .active-img{
            font-family: PingFangSC-Medium;
            font-size: 24px;
            color: #EDECD3;
            line-height: 35px;
            text-align: left;
            text-align: center;
        }
        .active-con .active-img img{
            margin:40px 0;
        }
        .active-con .active-img .text-lt{
            position: relative;
            z-index: 9;
            width: 990px;
            text-align: left;
            margin: auto;
        }
        .course-wrap{
            /* margin-top: 300px; */
            background:url("../../static/images/active_sign/bottom.png") no-repeat center bottom;
            background-size: 100%;
            width: 100%;
            /* height: 1700px; */
            position: relative;
        } 
        .course-wrap .sun{
            width: 20%;
            height: 200px;
            background: url("../../static/images/active_sign/sun.png") no-repeat center bottom;
            background-size: 100%;  
            position: absolute;
            left: 50%;
            top: 0; 
            margin-left: 20%;
            z-index: 10;
        }
        .course-wrap .bot-cloud{
            width: 17.1%;
            height: 190px;
            background: url("../../static/images/active_sign/bot_cloud.png") no-repeat center right;
            position: absolute;
            right: 0;
            bottom:900px;
            background-size: 100%;
            z-index: 10;
        }
        .course-wrap .inner{
            background: url("../../static/images/active_sign/course_pc.png") no-repeat center bottom;
            background-size: 100% 100%;
            position: relative;
            z-index: 9;
            height: 1460px;
        }
        .course-wrap .right-lines{
            width: 30%;
            height: 1280px;
            background: url("../../static/images/active_sign/bot_dark_lines.png") no-repeat center right;
            position: absolute;
            right: 0;
            top:-300px;
            z-index: 1;
        }
        .course-wrap .course{
            width: 31%;
            height: 160px;
            display: inline-block;
            margin-right: 2.7%;
            margin-bottom: 120px;
            /* background: rgba(0,0,0,.6) */
        }
        .course-wrap .cloud{
            width: 31%;
            height: 160px;
            display: inline-block;
            margin-right: 2.7%;
            margin-bottom: 120px;
            background: url("../../static/images/active_sign/cloud.png") no-repeat center bottom;
            position: relative;
            bottom:-10px;
        }
        .course-wrap .course a{
            display: inline-block;
            width: 100%;
            height: 100%;
        }
        .course-wrap .course-con{
            padding-top: 270px;
            padding-bottom: 70px;
            width: 65%;
            margin: auto;
        }
        .course-wrap .course:nth-of-type(3n){
            margin-right: 0;
        }
    }
    @media (min-width: 768px) and (max-width: 1200px) and (orientation: portrait),  (min-width: 768px) and (max-width: 1200px) and (orientation: landscape) {
        .inner{
            /* width: 1200px; */
            margin: 0 10px;
        }
        .active-wrap{
            position: relative;
        }
        .active-top{
            background: url("../../static/images/active_sign/head_dark_lines.png") no-repeat center top,url("../../static/images/active_sign/connect.png") no-repeat center bottom #0168CF;
            width: 100%;
            height: 810px;
            text-align: center;
            background-size: 100%;
        }
        .active-top .prompt{
            width: 56.1%;
            height: 56px;
        }
        .active-wrap .active-air{
            position: absolute;
            top:500px;
            left:50%;
            top: 700px;
            width: 92%;
            transform: translate3d(-50%,-50%,0)
        }
        .active-con{
            width: 100%;
            text-align: center;
            /* position: absolute;
            top: 700px; */
            padding-top: 150px;
            background:  #001278;
        }
        .active-con .top-cloud{
            width: 23.6%;
            height: 316px;
            background: url("../../static/images/active_sign/top_cloud.png") no-repeat center left;
            background-size: 100%;
            position: absolute;
            left: 0;
            top:1100px;
            z-index: 3;
        }
        .active-con .active-content{
            width: 490px;
            height: 105px;
            position: absolute;
            left: 50%;
            margin-left: -150px;
            top:700px;
            margin-top: -50px;
            font-family: PingFangSC-Medium;
            font-size: 18px;
            color: #EDECD3;
            line-height: 26px;
            text-align: left;
        }
        .active-con .active-img{
            font-family: PingFangSC-Medium;
            font-size: 18px;
            color: #EDECD3;
            line-height: 26px;
            text-align: left;
            text-align: center;
        }
        .active-con .active-img .time-img{
            width: 87.5%;
            height: 140px;
            margin-bottom: 0
        }
        .active-con .active-img img{
            margin:40px 0;
            width: 36.8%;
            height: 54px;
        }
        .active-con .active-img .text-lt{
            position: relative;
            z-index: 9;
            width: 100%;
            text-align: left;
            margin: auto;
        }
        .course-wrap{
            /* margin-top: 300px; */
            background:url("../../static/images/active_sign/bottom.png") no-repeat center bottom;
            background-size: 100%;
            width: 100%;
            /* height: 1700px; */
            position: relative;
        } 
        .course-wrap .sun{
            width: 20%;
            height: 200px;
            background: url("../../static/images/active_sign/sun.png") no-repeat center bottom;
            background-size: 100%;  
            position: absolute;
            left: 50%;
            top: -40px; 
            margin-left: 20%;
            z-index: 10;
        }
        .course-wrap .bot-cloud{
            width: 17.1%;
            height: 190px;
            background: url("../../static/images/active_sign/bot_cloud.png") no-repeat center right;
            position: absolute;
            right: 0;
            bottom:400px;
            background-size: 100%;
            z-index: 10;
        }
        .course-wrap .inner{
            background: url("../../static/images/active_sign/course_pc.png") no-repeat center bottom;
            background-size: 100% 100%;
            position: relative;
            z-index: 9;
            height: 910px;
        }
        .course-wrap .right-lines{
            width: 30%;
            height: 1280px;
            background: url("../../static/images/active_sign/bot_dark_lines.png") no-repeat center right;
            background-size: 100%;
            position: absolute;
            right: 0;
            top:-300px;
            z-index: 1;
        }
        .course-wrap .course{
            /* background: rgba(0,0,0,.6); */
            width: 31%;
            height: 100px;
            display: inline-block;
            margin-right: 2.7%;
            margin-bottom: 70px;
        }
        .course-wrap .cloud{
            width: 31%;
            height: 100px;
            display: inline-block;
            margin-right: 2.7%;
            margin-bottom: 70px;
            background: url("../../static/images/active_sign/cloud.png") no-repeat center bottom;
            position: relative;
            bottom:-10px;
            background-size: 100%;
        }
        .course-wrap .course a{
            display: inline-block;
            width: 100%;
            height: 100%;
        }
        .course-wrap .course-con{
            padding-top: 170px;
            padding-bottom: 60px;
            width: 65%;
            margin: auto;
        }
        .course-wrap .course:nth-of-type(3n){
            margin-right: 0;
        }
    
    }
    @media (min-width: 768px) and (max-width: 1200px) and (orientation: landscape) {
        .active-wrap .active-air{
            top:890px;
        }
        .active-top .prompt {
            height: 80px;
        }
        .active-con .active-content{
            top:900px;
        }
        .active-top{
            height: 1150px;
        }
        .active-con .active-img .time-img{
            height: 165px;
        }
        .active-con .active-img img{
            width: 41%;
            height: 80px;
        }
        .course-wrap .course{
            height: 140px;
        }
        .course-wrap .cloud{
            height: 130px;
        }
        .course-wrap .course-con{
            padding-top: 220px;
            padding-bottom: 80px;
        }
        .course-wrap .course{
            margin-bottom: 91px;
        }
        .course-wrap .sun{
            top:-15px;
        }
        .course-wrap .bot-cloud{
            bottom: 1400px;
        }
        .active-con .top-cloud{
            top:1500px;
        }
        .course-wrap .inner{
            height: 1224px;
        }
    }
</style>
