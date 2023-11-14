<template>
  <view>
    <!-- 导航栏 -->
    <view class="nav">
      <picker
        class="xuanzhe"
        @change="changeweek($event, week)"
        :value="index"
        :range="week"
        :range-key="'wee'"
        >{{ beginweek }}
      </picker>
    </view>
    <view class="empty"></view>
    <!-- 日期 -->
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
    <!-- 课程 -->
    <!-- id选择器 -->
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
import fullScreenVideoAdVue from "../../../../my-project/src/pages/API/full-screen-video-ad/full-screen-video-ad.vue";
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
      console.log(this.data);
      if (this.data != null) {
        this.getLesson();
      } else {
        console.log("false");
      }
    });
  },
  mounted() {
    this.getweek();
    // this.getLesson();
  },
  computed: {},
  methods: {
    //突出当前时间
    breakout(NowWeek) {
      const date1 = new Date();
      console.log(NowWeek);
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
    changeweek(e, week) {
      console.log(e);
      // 周数下标
      const index = e.detail.value;
      console.log(index);
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
    },
    //渲染课程
    getLesson() {
      for (let i = 0; i < this.data.length; i++) {
        //正则表达式提取出数值
        // const sessionRegex = /(\d+)-(\d+)/;
        // const matches = sessionRegex.exec(this.lesson[i].session);
        // const classlong = (matches[2] - matches[1] + 1) * 100;
        // const weekDate = this.lesson[i].weekDate;
        // const session = parseInt(matches[1], 10);
        // //渲染到对应位置
        // this.cla[weekDate].lesson[(session - 1) / 2].marginTop =
        //   (session - 1) * 100;
        // //渲染课程名
        // this.cla[weekDate].lesson[(session - 1) / 2].course.courseName =
        //   this.lesson[i].courseName;
        // //渲染课程地点
        // this.cla[weekDate].lesson[(session - 1) / 2].course.classRoom =
        //   "@" + this.lesson[i].classRoom;
        // //渲染课程教师名称
        // this.cla[weekDate].lesson[(session - 1) / 2].course.teacher =
        //   "@" + this.lesson[i].teacher;
        // //渲染课程长度
        // this.cla[weekDate].lesson[(session - 1) / 2].height = classlong;
        // //随机选取颜色
        // const n = Math.floor(Math.random() * this.getcolor.length);
        // this.cla[weekDate].lesson[(session - 1) / 2].color = this.getcolor[n];

        const sessionRegex = /(\d+)-(\d+)/;
        const matches = sessionRegex.exec(this.data[i].session);
        const classlong = (matches[2] - matches[1] + 1) * 100;
        const weekDate = this.lesson[i].weekDate;
        const session = parseInt(matches[1], 10);
        //渲染到对应位置
        this.cla[weekDate].lesson[(session - 1) / 2].marginTop =
          (session - 1) * 100;
        //渲染课程名
        this.cla[weekDate].lesson[(session - 1) / 2].course.courseName =
          this.data[i].courseName;
        //渲染课程地点
        this.cla[weekDate].lesson[(session - 1) / 2].course.classRoom =
          "@" + this.data[i].classRoom;
        //渲染课程教师名称
        this.cla[weekDate].lesson[(session - 1) / 2].course.teacher =
          "@" + this.data[i].teacher;
        //渲染课程长度
        this.cla[weekDate].lesson[(session - 1) / 2].height = classlong;
        //随机选取颜色
        const n = Math.floor(Math.random() * this.getcolor.length);
        this.cla[weekDate].lesson[(session - 1) / 2].color = this.getcolor[n];
      }
    },
    signIn(index1, index2) {
      this.display1 = "block";
      console.log(index1 + "--" + index2);
      const course = this.cla[index1].lesson[index2].course;
      this.ClickCourseName = course.courseName;
      this.ClickClassRoom = course.classRoom;
      this.ClickTeacher = course.teacher;
    },
    cancelTanchuang() {
      this.display1 = "none";
    },
    // 跳转到签到页面
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
