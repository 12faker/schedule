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
      <button class="shouye-mid" :disabled="isDisabled" @tap="getLesson()">
        同步课表
      </button>
      <button class="shouye-bottom" :disabled="isDisabled" @tap="quitlogin()">
        退出登录
      </button>
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
      isDisabled: false, // 默认同步课表按钮可用
      logindisplay: "block",
      homedisplay: "none",
      usernumber: "",
      password: "",
      data: "",
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
    getLesson() {
      if (this.data == "") {
        this.sendMsg();
      } else {
        //获取之后，添加确认是否重复获取的功能
        uni
          .showModal({
            title: "确认操作",
            content: "你已获取了课表,确定要再次获取吗",
          })
          .then((res) => {
            if (res.confirm) {
              // 用户点击了确认按钮，执行函数
              // 在这里写你想要执行的代码
              this.sendMsg();
            } else {
              // 用户点击了取消按钮，不执行函数
              console.log("取消执行");
            }
          })
          .catch((err) => {
            console.error(err);
          });
      }
    },
    sendMsg() {
      this.isDisabled = true;
      uni.showLoading({
        title: "获取课表中...", //显示加载中
      });
      uni.hideTabBar();
      uni.request({
        url: "http://localhost:8080/Ats", // 你的后端接口地址
        method: "GET",
        timeout: 25000, //请求允许时间25秒
        success: (res) => {
          // Check for potential errors in the response
          if (res.data) {
            // Request successful handling
            uni.showToast({
              title: "获取成功",
              icon: "none",
            });
            this.data = 1;
            bus.$emit("share", res.data.data);
            console.log(res);
          } else {
            console.error("Empty response data");
          }
        },
        fail: (err) => {
          // 请求失败处理
          uni.showToast({
            title: "超时，获取失败",
            icon: "none",
          });
          console.error(err);
        },
        complete: () => {
          // 隐藏加载提示
          uni.hideLoading();
          uni.showTabBar();
          this.isDisabled = false;
        },
      });
    },
  },
  watch: {},
});
</script>
<style scoped src="./my.css"></style>
