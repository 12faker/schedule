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
      <button class="shouye-bottom" @tap="quitlogin()">退出登录</button>
    </view>
  </view>
</template>

<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  components: {},
  data() {
    return {
      logindisplay: "block",
      homedisplay: "none",
      usernumber: "",
      password: "",
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
  },
  watch: {},
});
</script>
<style scoped src="./my.css"></style>
