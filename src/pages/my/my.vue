<template>
  <view>
    <view class="input" :style="{ display: logindisplay }">
      <view class="input1">
        <span>账号：</span>
        <input type="text" v-model="usernumber" />
      </view>
      <view class="input2">
        密码：
        <input type="password" v-model="password" />
      </view>
      <button class="login" @tap="gologin()">登录</button>
    </view>
    <view class="shouye" :style="{ display: homedisplay }">
      <view class="shouye-front"></view>
      <view class="shouye-middle"></view>
      <button class="shouye-mid" @tap="sendMsg()">同步课表</button>
      <button class="shouye-bottom" @tap="quitlogin()">退出登录</button>
    </view>
  </view>
</template>

<script>
import Vue from "vue";
import bus from "../eventBus.js";
export default Vue.extend({
  components: {},
  data() {
    return {
      logindisplay: "block",
      homedisplay: "none",
      usernumber: "",
      password: "",
      data: [
        {
          teacher: "王老师",
          classRoom: "大学城电子楼412A",
          weekDate: "1",
          session: "2-4节",
          courseName: "计算机组成",
          weekTimes: "1-10周",
        },
        {
          teacher: "陈老师",
          classRoom: "大学城理科南512",
          weekDate: "1",
          session: "9-11节",
          courseName: "高等数学",
          weekTimes: "2-3周,5-7周.9-16周",
        },
        {
          teacher: "胡老师",
          classRoom: "大学城理科南211",
          weekDate: "1",
          session: "5-6节",
          courseName: "程序",
          weekTimes: "1-5周,6周,8-12周",
        },
        {
          teacher: "王老师",
          classRoom: "大学城理科南311",
          weekDate: "2",
          session: "9-11节",
          courseName: "计组",
          weekTimes: "1-5周",
        },
        {
          teacher: "李老师",
          classRoom: "大学城理科南211",
          weekDate: "2",
          session: "6-8节",
          courseName: "程序",
          weekTimes: "1-5周",
        },
        {
          teacher: "王老师",
          classRoom: "大学城理科南311",
          weekDate: "3",
          session: "3-4节",
          courseName: "计组",
          weekTimes: "1-16周",
        },
        {
          teacher: "王老师",
          classRoom: "大学城理科南311",
          weekDate: "4",
          session: "9-10节",
          courseName: "计组",
          weekTimes: "2-7周",
        },
        {
          teacher: "王老师",
          classRoom: "大学城理科南311",
          weekDate: "5",
          session: "5-7节",
          courseName: "计组",
          weekTimes: "4-5周",
        },
      ],
    };
  },
  computed: {},
  methods: {
    gologin() {
      if (this.usernumber == 123 && this.password == 123) {
        this.homedisplay = "block";
        this.logindisplay = "none";
        console.log("登录成功");
      } else console.log("登录失败");
    },
    quitlogin() {
      this.homedisplay = "none";
      this.logindisplay = "block";
    },
    sendMsg() {
      bus.$emit("share", this.data);
    },
  },
  watch: {},
});
</script>
<style scoped src="./my.css"></style>
