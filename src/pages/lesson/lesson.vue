<template>
  <view>
    <!-- 导航栏 -->
    <view class="nav" :style="{ height: screensafe + parseInt(150) + 'rpx' }">
      <picker
        class="xuanzhe"
        @change="changeweek($event, week)"
        :value="index"
        :range="week"
        :range-key="'wee'"
        :style="{ marginTop: screensafe + parseInt(70) + 'rpx' }"
        >{{ beginweek }}
      </picker>
    </view>
    <view
      class="empty"
      :style="{ height: screensafe + parseInt(150) + 'rpx' }"
    ></view>
    <!-- 日期 -->
    <view class="date1">
      <view
        class="date"
        v-for="(tim, index) in time"
        :style="{ width: tim.width }"
        :key="index"
      >
        <view class="date-month"> {{ tim.week }}</view>
        <view
          class="date-date"
          :style="{ backgroundColor: tim.backgroundcolor, color: tim.color }"
        >
          {{ tim.date }}</view
        >
      </view>
    </view>
    <!-- 课程 -->
    <!-- id选择器 -->
    <view class="lesson1">
      <view
        class="lesson"
        v-for="(clas, index1) in cla"
        :key="index1"
        :style="{ width: clas.width }"
      >
        <view
          v-for="(lesso, index2) in clas.lesson"
          @tap="signIn(index1, index2)"
          :key="index2"
          :id="clas.id + '-' + lesso.id"
          :style="{
            height: lesso.height + 'rpx',
            marginTop: lesso.marginTop + 'rpx',
            backgroundColor: lesso.color,
          }"
        >
          {{ lesso.text }}
          {{ lesso.course.courseName }}<br />
          {{ lesso.course.classRoom }}<br />
          {{ lesso.course.teacher }}<br />
          <!-- {{ lesso.course.teacher }} -->
        </view>
      </view>
    </view>
    <!--弹窗 -->
    <view class="tanchaung" :style="{ display: display1 }">
      <view class="t-tanchuang"
        ><view> </view>
        <button class="cancel" @tap="cancelTanchuang()">&times;</button>
        <view>
          {{ ClickCourseName }}<br />
          {{ ClickClassRoom }}<br />
          {{ ClickTeacher }}<br />
        </view>
        <button class="qiandao" @tap="toLogin()">签到</button>
      </view>
    </view>
  </view>
</template>

<script>
import Vue from "vue";
//import fullScreenVideoAdVue from "../../../../my-project/src/pages/API/full-screen-video-ad/full-screen-video-ad.vue";
import index from "../index/index.vue";
import bus from "../eventBus.js";
export default Vue.extend({
  components: {
    index,
  },
  data() {
    return {
      index: 0,
      beginweek: "第1周",
      begindate: "2023-9-4",
      display1: "none",
      ClickCourseName: "",
      ClickClassRoom: "",
      ClickTeacher: "",
      ClickColor: "",
      data: "",
      screensafe: "",
      //存储当前周数
      NowWeek: "",
      getcolor: [
        "#00ffff",
        "#ffd1dc",
        "#1cd879",
        "#ff8f13",
        "#ff6a9b",
        "#ffcf4c",
        "#f99aa0",
        "#2cb5fc",
        "#ff8f6b",
        "#dcd0ff",
        "#32c9de",
        "#16ae9c",
        "#f5de19",
      ],
      week: [
        { id: 1, wee: "第1周" },
        { id: 2, wee: "第2周" },
        { id: 3, wee: "第3周" },
        { id: 4, wee: "第4周" },
        { id: 5, wee: "第5周" },
        { id: 6, wee: "第6周" },
        { id: 7, wee: "第7周" },
        { id: 8, wee: "第8周" },
        { id: 9, wee: "第9周" },
        { id: 10, wee: "第10周" },
        { id: 11, wee: "第11周" },
        { id: 12, wee: "第12周" },
        { id: 13, wee: "第13周" },
        { id: 14, wee: "第14周" },
        { id: 15, wee: "第15周" },
        { id: 16, wee: "第16周" },
        { id: 17, wee: "第17周" },
        { id: 18, wee: "第18周" },
        { id: 19, wee: "第19周" },
        { id: 20, wee: "第20周" },
      ],
      time: [
        {
          id: 0,
          week: "10",
          date: "月",
          width: "9%",
          backgroundcolor: "",
          color: "",
        },
        {
          id: 1,
          week: "一",
          date: "1",
          width: "13%",
          backgroundcolor: "",
          color: "",
        },
        {
          id: 2,
          week: "二",
          date: "2",
          width: "13%",
          backgroundcolor: "",
          color: "",
        },
        {
          id: 3,
          week: "三",
          date: "3",
          width: "13%",
          backgroundcolor: "",
          color: "",
        },
        {
          id: 4,
          week: "四",
          date: "4",
          width: "13%",
          backgroundcolor: "",
          color: "",
        },
        {
          id: 5,
          week: "五",
          date: "5",
          width: "13%",
          backgroundcolor: "",
          color: "",
        },
        {
          id: 6,
          week: "六",
          date: "6",
          width: "13%",
          backgroundcolor: "",
          color: "",
        },
        {
          id: 7,
          week: "日",
          date: "7",
          width: "13%",
          backgroundcolor: "",
          color: "",
        },
      ],
      cla: [
        {
          id: "z",
          width: "9%",
          lesson: [
            {
              id: "a",
              text: "1",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "b",
              text: "2",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "c",
              text: "3",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "d",
              text: "4",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "e",
              text: "5",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "f",
              text: "6",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "g",
              text: "7",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "h",
              text: "8",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "i",
              text: "9",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "j",
              text: "10",
              height: "",
              marginTop: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "k",
              text: "11",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
          ],
        },
        {
          id: "a",
          width: "13%",
          lesson: [
            {
              id: "a",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "b",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "c",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "d",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "e",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
          ],
        },
        {
          id: "b",
          width: "13%",
          lesson: [
            {
              id: "a",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "b",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "c",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "d",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "e",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
          ],
        },
        {
          id: "c",
          width: "13%",
          lesson: [
            {
              id: "a",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "b",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "c",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "d",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "e",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
          ],
        },
        {
          id: "d",
          width: "13%",
          lesson: [
            {
              id: "a",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "b",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "c",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "d",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "e",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
          ],
        },
        {
          id: "e",
          width: "13%",
          lesson: [
            {
              id: "a",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "b",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "c",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "d",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "e",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
          ],
        },
        {
          id: "f",
          width: "13%",
          lesson: [
            {
              id: "a",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "b",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "c",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "d",
              text: "",
              height: "",
              marginTop: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "e",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
          ],
        },
        {
          id: "g",
          width: "13%",
          lesson: [
            {
              id: "a",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "b",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "c",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "d",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
            {
              id: "e",
              text: "",
              height: "",
              marginTop: "",
              color: "",
              course: {
                teacher: "",
                classRoom: "",
                weekDate: "",
                session: "",
                courseName: "",
                weekTimes: "",
              },
            },
          ],
        },
      ],
      lesson: [
        {
          teacher: "王老师",
          classRoom: "大学城电子楼412A",
          weekDate: "1",
          session: "5-6节",
          courseName: "计算机组成",
          weekTimes: "9-16周",
        },
        {
          teacher: "陈老师",
          classRoom: "大学城理科南512",
          weekDate: "1",
          session: "9-11节",
          courseName: "高等数学",
          weekTimes: "9-16周",
        },
        {
          teacher: "林老师",
          classRoom: "大学城理科南210",
          weekDate: "2",
          session: "1-2节",
          courseName: "程序",
          weekTimes: "1-5周",
        },
      ],
    };
  },
  created() {
    bus.$on("share", (val) => {
      this.data = val;
      if (this.data != null) {
        this.getLesson();
      } else {
        console.log("false");
      }
    });
  },
  mounted() {
    this.getweek();
    this.safe();
    // this.getLesson();
  },
  computed: {},
  methods: {
    //突出当前时间
    safe() {
      const { safeAreaInsets } = uni.getSystemInfoSync();
      this.screensafe = safeAreaInsets.top;
    },
    breakout(NowWeek) {
      const date1 = new Date();
      if (NowWeek == this.NowWeek) {
        if (date1.getDay() == 0) {
          this.time[7].backgroundcolor = "#00ffff";
          this.time[7].color = "#f2f9ff";
        } else {
          this.time[date1.getDay()].backgroundcolor = "#00ffff";
          this.time[date1.getDay()].color = "#f2f9ff";
        }
      } else {
        if (date1.getDay() == 0) {
          this.time[7].backgroundcolor = "";
          this.time[7].color = "";
        } else {
          this.time[date1.getDay()].backgroundcolor = "";
          this.time[date1.getDay()].color = "";
        }
      }
    },
    //渲染当前一周时间
    getweek() {
      const oneDay = 24 * 60 * 60 * 1000;
      const begindate1 = new Date(this.begindate);
      const date1 = new Date();
      const time1 = begindate1.getTime();
      const time2 = date1.getTime();
      const diffDays = Math.floor(Math.abs((time2 - time1) / oneDay));
      const zhoushu = Math.floor(diffDays / 7);
      //记录当前周数
      this.NowWeek = zhoushu + 1;
      this.beginweek = this.week[zhoushu].wee;
      let differ = 7 * zhoushu;
      //选择的Date对象
      let selectdate = begindate1.setDate(begindate1.getDate() + differ);
      //将时间戳转换为Date对象
      let selectdate1 = new Date(selectdate);
      this.time[0].week = selectdate1.getMonth() + 1;
      //逐个渲染上去
      for (let i = 0; i < 7; i++) {
        //创建新的日期对象
        let selectdate2 = new Date(selectdate1);
        selectdate2.setDate(selectdate2.getDate() + i);
        this.time[i + 1].date = selectdate2.getDate();
      }
      this.breakout(parseInt(zhoushu) + parseInt(1));
    },
    //渲染自己切换的时间
    //---------------------------------------------------------------------
    changeweek(e, week) {
      // 周数下标
      const index = e.detail.value;
      //将选择的周数渲染上去
      this.beginweek = week[index].wee;
      // 相差天数
      let differ = 7 * index;
      // 起始点的Date对象
      let begindate1 = new Date(this.begindate);
      //选择的Date对象
      let selectdate = begindate1.setDate(begindate1.getDate() + differ);
      //将时间戳转换为Date对象
      let selectdate1 = new Date(selectdate);
      this.time[0].week = selectdate1.getMonth() + 1;
      //逐个渲染上去
      for (let i = 0; i < 7; i++) {
        //创建新的日期对象
        let selectdate2 = new Date(selectdate1);
        selectdate2.setDate(selectdate2.getDate() + i);
        this.time[i + 1].date = selectdate2.getDate();
      }
      this.breakout(parseInt(index) + parseInt(1));
      //清除原有课程，渲染新课程
      for (let i = 1; i <= 7; i++) {
        for (let j = 0; j < 5; j++) {
          this.cla[i].lesson[j].height = "";
          this.cla[i].lesson[j].marginTop = "";
          this.cla[i].lesson[j].color = "";
          for (let key in this.cla[i].lesson[j].course) {
            this.cla[i].lesson[j].course[key] = "";
          }
        }
      }
      this.getLesson();
    },
    //渲染课程
    //---------------------------------------------------------------------
    getLesson() {
      let n;
      for (let i = 0; i < this.data.length; i++) {
        //正则表达式提取数字
        const pattern = /\d+-\d+|\d+/g;
        const pattern1 = /\d+/;
        const sessionRegex = /(\d+)-(\d+)/;
        let work = 0;
        let matches1 = this.data[i].weekTimes.match(pattern);
        let selectWeek = this.beginweek.match(pattern1);
        //判断该周是否有该课程
        for (let i = 0; i < matches1.length; i++) {
          //console.log(matches1[i]);
          if (matches1[i].includes("-")) {
            let Week = sessionRegex.exec(matches1[i]);
            if (
              (parseInt(Week[1]) <= parseInt(selectWeek[0])) &
              (parseInt(Week[2]) >= parseInt(selectWeek[0]))
            )
              work++;
          } else {
            if (parseInt(matches1[i]) == parseInt(selectWeek[0])) work++;
          }
        }
        //-------------------------------------------------------------------------
        if (work > parseInt(0)) {
          let matches = sessionRegex.exec(this.data[i].session);
          const classlong = (matches[2] - matches[1] + 1) * 100;
          const weekDate = this.data[i].weekDate;
          const session = parseInt(matches[1], 10);
          const session1 = (session - 1) / 2;
          //渲染到对应位置,未采用定位，根据前一个元素判断渲染到哪个位置
          //渲染第1-2节的课
          if (session1 == 0) {
            this.cla[weekDate].lesson[session1].marginTop = (session - 1) * 100;
          } else {
            //渲染第9-10节的课
            if (session1 == 4) {
              let k = 0;
              for (let j = 0; j < 4; j++) {
                if (this.cla[weekDate].lesson[j].course.courseName != "") {
                  k = j + 1;
                }
              }
              this.cla[weekDate].lesson[session1].marginTop =
                (session1 - k) * 200;
            } else {
              //渲染第2-4节和6-8节的课程
              if (session1 == 0.5 || session1 == 2.5) {
                let n = Math.ceil(session1);
                if (session1 == 0.5) {
                  this.cla[weekDate].lesson[n].marginTop = session1 * 200;
                } else {
                  let k = 0;
                  for (let i = 0; i < 2; i++) {
                    if (this.cla[weekDate].lesson[i].course.courseName != "") {
                      k = i + 1;
                    }
                  }
                  this.cla[weekDate].lesson[n].marginTop = (session1 - k) * 200;
                  //修改下一个课程
                  if (
                    this.cla[weekDate].lesson[n + 1].course.courseName != ""
                  ) {
                    this.cla[weekDate].lesson[n + 1].marginTop = 0;
                  }
                }
              } else {
                let k = 0;
                for (let j = 0; j < session1; j++) {
                  if (this.cla[weekDate].lesson[j].course.courseName != "") {
                    k = j + 1;
                  }
                }
                this.cla[weekDate].lesson[session1].marginTop =
                  (session1 - k) * 200;
                let k1 = 0;
                let j = 0;
                for (j = 4; j > session1; j--) {
                  if (this.cla[weekDate].lesson[j].course.courseName != "") {
                    k1 = j;
                  }
                }
                if (k1 != 0) {
                  const matches1 = sessionRegex.exec(
                    this.cla[weekDate].lesson[k1].course.session
                  );
                  if (matches1[1] != 6) {
                    this.cla[weekDate].lesson[k1].marginTop =
                      (k1 - session1) * 200 - classlong;
                  } else {
                    this.cla[weekDate].lesson[k1].marginTop =
                      (k1 - session1 - parseFloat(0.5)) * 200 - classlong;
                  }
                }
              }
            }
          }
          //渲染课程名
          this.cla[weekDate].lesson[Math.ceil(session1)].course.courseName =
            this.data[i].courseName;
          //渲染课程地点
          this.cla[weekDate].lesson[Math.ceil(session1)].course.classRoom =
            "@" + this.data[i].classRoom;
          //渲染课程教师名称
          this.cla[weekDate].lesson[Math.ceil(session1)].course.teacher =
            "@" + this.data[i].teacher;
          //渲染课程长度
          this.cla[weekDate].lesson[Math.ceil(session1)].height = classlong;
          //课程节数赋值
          this.cla[weekDate].lesson[Math.ceil(session1)].course.session =
            this.data[i].session;
          //随机选取颜色
          let tof = true;
          while (tof) {
            console.log(1);
            let n1 = Math.floor(Math.random() * this.getcolor.length);
            if (n != n1) {
              n = n1;
              this.cla[weekDate].lesson[Math.ceil(session1)].color =
                this.getcolor[n];
              tof = false;
            }
          }
        }
      }
    },
    //---------------------------------------------------------------------
    signIn(index1, index2) {
      if (this.cla[index1].lesson[index2].course.courseName != "") {
        this.display1 = "block";
        const course = this.cla[index1].lesson[index2].course;
        this.ClickCourseName = course.courseName;
        this.ClickClassRoom = course.classRoom;
        this.ClickTeacher = course.teacher;
      }
    },
    //---------------------------------------------------------------------
    cancelTanchuang() {
      this.display1 = "none";
    },
    // 跳转到签到页面
    //---------------------------------------------------------------------
    toLogin() {
      uni.switchTab({
        url: "/pages/index/index",
      });
    },
  },
  watch: {},
});
</script>

<style scoped src="./leeson.css"></style>
