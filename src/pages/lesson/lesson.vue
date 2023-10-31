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
      <view :style="{ width: tim.width }"> {{ tim.week }}</view>
      <view :style="{ width: tim.width }"> {{ tim.date }}</view>
    </view>
    <!-- 课程 -->
    <!-- id选择器 -->
    <view
      class="lesson"
      v-for="(clas, index) in cla"
      :key="index"
      :style="{ width: clas.width }"
    >
      <view
        v-for="(lesso, index) in clas.lesson"
        @tap="signIn(lesso.text)"
        :key="index"
        :id="clas.id + '-' + lesso.id"
        :style="{
          height: lesso.height + 'rpx',
          marginTop: lesso.marginTop + 'rpx',
        }"
      >
        {{ lesso.text }}
      </view>
    </view>

    <!--弹窗 -->
    <view class="tanchaung" :style="{ display: display1 }">
      <view class="t-tanchuang"
        ><view> </view>
        <button class="cancel" @tap="cancelTanchuang()">&times;</button>
        <view>{{ nowlesson }}</view>
        <button class="qiandao" @tap="toLogin()">签到</button>
      </view>
    </view>
  </view>
</template>

<script>
import Vue from "vue";
import fullScreenVideoAdVue from "../../../../my-project/src/pages/API/full-screen-video-ad/full-screen-video-ad.vue";
export default Vue.extend({
  components: {},
  data() {
    return {
      index: 0,
      beginweek: "第1周",
      begindate: "2023-9-4",
      display1: "none",
      nowlesson: "",
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
        { id: 0, week: "10月", date: "", width: "9%" },
        { id: 1, week: "一", date: "1", width: "13%" },
        { id: 2, week: "二", date: "2", width: "13%" },
        { id: 3, week: "三", date: "3", width: "13%" },
        { id: 4, week: "四", date: "4", width: "13%" },
        { id: 5, week: "五", date: "5", width: "13%" },
        { id: 6, week: "六", date: "6", width: "13%" },
        { id: 7, week: "日", date: "7", width: "13%" },
      ],
      cla: [
        {
          id: "z",
          width: "9%",
          lesson: [
            { id: "a", text: "1", height: "", marginTop: "" },
            { id: "b", text: "2", height: "", marginTop: "" },
            { id: "c", text: "3", height: "", marginTop: "" },
            { id: "d", text: "4", height: "", marginTop: "" },
            { id: "e", text: "5", height: "", marginTop: "" },
            { id: "f", text: "6", height: "", marginTop: "" },
            { id: "g", text: "7", height: "", marginTop: "" },
            { id: "h", text: "8", height: "", marginTop: "" },
            { id: "i", text: "9", height: "", marginTop: "" },
            { id: "j", text: "10", height: "", marginTop: "" },
            { id: "k", text: "11", height: "", marginTop: "" },
          ],
        },
        {
          id: "a",
          width: "13%",
          lesson: [
            { id: "a", text: "", height: "", marginTop: "" },
            { id: "b", text: "", height: "", marginTop: "" },
            { id: "c", text: "", height: "", marginTop: "" },
            { id: "d", text: "", height: "", marginTop: "" },
            { id: "e", text: "", height: "", marginTop: "" },
          ],
        },
        {
          id: "b",
          width: "13%",
          lesson: [
            { id: "a", text: "", height: "", marginTop: "" },
            { id: "b", text: "", height: "", marginTop: "" },
            { id: "c", text: "", height: "", marginTop: "" },
            { id: "d", text: "", height: "", marginTop: "" },
            { id: "e", text: "", height: "", marginTop: "" },
          ],
        },
        {
          id: "c",
          width: "13%",
          lesson: [
            { id: "a", text: "", height: "", marginTop: "" },
            { id: "b", text: "", height: "", marginTop: "" },
            { id: "c", text: "", height: "", marginTop: "" },
            { id: "d", text: "", height: "", marginTop: "" },
            { id: "e", text: "", height: "", marginTop: "" },
          ],
        },
        {
          id: "d",
          width: "13%",
          lesson: [
            { id: "a", text: "", height: "", marginTop: "" },
            { id: "b", text: "", height: "", marginTop: "" },
            { id: "c", text: "", height: "", marginTop: "" },
            { id: "d", text: "", height: "", marginTop: "" },
            { id: "e", text: "", height: "", marginTop: "" },
          ],
        },
        {
          id: "e",
          width: "13%",
          lesson: [
            { id: "a", text: "", height: "", marginTop: "" },
            { id: "b", text: "", height: "", marginTop: "" },
            { id: "c", text: "", height: "", marginTop: "" },
            { id: "d", text: "", height: "", marginTop: "" },
            { id: "e", text: "", height: "", marginTop: "" },
          ],
        },
        {
          id: "f",
          width: "13%",
          lesson: [
            { id: "a", text: "", height: "", marginTop: "" },
            { id: "b", text: "", height: "", marginTop: "" },
            { id: "c", text: "", height: "", marginTop: "" },
            { id: "d", text: "", height: "", marginTop: "" },
            { id: "e", text: "", height: "", marginTop: "" },
          ],
        },
        {
          id: "g",
          width: "13%",
          lesson: [
            { id: "a", text: "", height: "", marginTop: "" },
            { id: "b", text: "", height: "", marginTop: "" },
            { id: "c", text: "", height: "", marginTop: "" },
            { id: "d", text: "", height: "", marginTop: "" },
            { id: "e", text: "", height: "", marginTop: "" },
          ],
        },
      ],
      course: [{ name: "数学", week: 4, jie: 5, long: 2 }],
    };
  },
  mounted() {
    this.getweek();
    this.getLesson();
  },
  computed: {},
  methods: {
    //渲染当前时间
    getweek() {
      const oneDay = 24 * 60 * 60 * 1000;
      const begindate1 = new Date(this.begindate);
      const date1 = new Date();
      const time1 = begindate1.getTime();
      const time2 = date1.getTime();
      const diffDays = Math.floor(Math.abs((time2 - time1) / oneDay));
      console.log(diffDays);
      const zhoushu = Math.floor(diffDays / 7);
      this.beginweek = this.week[zhoushu].wee;
      let differ = 7 * zhoushu;
      console.log(zhoushu);
      //选择的Date对象
      let selectdate = begindate1.setDate(begindate1.getDate() + differ);
      //将时间戳转换为Date对象
      let selectdate1 = new Date(selectdate);
      this.time[0].week = selectdate1.getMonth() + 1 + "月";
      //逐个渲染上去
      for (let i = 0; i < 7; i++) {
        //创建新的日期对象
        let selectdate2 = new Date(selectdate1);
        selectdate2.setDate(selectdate2.getDate() + i);
        this.time[i + 1].date = selectdate2.getDate();
      }
    },
    //渲染自己切换的时间
    changeweek(e, week) {
      console.log(e);
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
      this.time[0].week = selectdate1.getMonth() + 1 + "月";
      //逐个渲染上去
      for (let i = 0; i < 7; i++) {
        //创建新的日期对象
        let selectdate2 = new Date(selectdate1);
        selectdate2.setDate(selectdate2.getDate() + i);
        this.time[i + 1].date = selectdate2.getDate();
      }
    },
    //渲染课程
    getLesson() {
      if (this.course[0].week == 4 && this.course[0].jie == 5) {
        this.cla[this.course[0].week].lesson[
          (this.course[0].jie - 1) / 2
        ].text = this.course[0].name;
        this.cla[this.course[0].week].lesson[
          (this.course[0].jie - 1) / 2
        ].marginTop = (this.course[0].jie - 1) * 100;
      }
    },
    signIn(text) {
      console.log(1);
      this.display1 = "block";
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
