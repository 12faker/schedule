<template>
  <view>
    <view
      ><button class="a" @tap="phoneWH()">点击</button>
      <button class="b" @tap="phoneWH()">点击</button></view
    >
  </view>
</template>

<script>
import Vue from "vue";
export default Vue.extend({
  components: {},
  data() {
    return {};
  },
  onLoad() {},
  onReady() {},
  mounted() {},
  methods: {
    phoneWH() {
      // 获取系统信息
      uni.getSystemInfo({
        success: function (res) {
          console.log(res.windowWidth);
          console.log(res.windowHeight);
        },
      });
    },
  },
  computed: {},
});
</script>

<style scoped>
view .a {
  height: 100px;
}
view .b {
  height: 150rpx;
}
</style>
