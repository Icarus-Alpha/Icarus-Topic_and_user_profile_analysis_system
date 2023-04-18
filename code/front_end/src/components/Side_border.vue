<template>
  <div class="side">
    <div class="side_background"></div>
    <div class="logo" @click="ToHome" href="#" title="返回主菜单"></div>
    <div class="wb" @click="ToWB" href="#" title="返回舆情分析页">
      <svg class="icon" aria-hidden="true">
        <use xlink:href="#icon-weibo-copy"></use>
      </svg>
    </div>
    <div class="user">
      <svg class="icon" aria-hidden="true">
        <use xlink:href="#icon-yonghu"></use>
      </svg>
    </div>
  </div>
</template>

<script>
export default {
  name: "side_border",
  methods: {
    ToWB() {
      this.$router.push({
        path: "/wb",
      });
    },
    ToHome() {
      this.$router.push({
        path: "/home",
      });
    },
  },
};
</script>

<style scoped>
.side {
  width: 100%;
  height: 100%;
}
.side_background {
  background: transparent;
  width: 50px;
  height: 100%;
}
.logo {
  position: relative;
  top: -100vh;
  width: 50px;
  height: 6.5%;
  background: #61DAFB url("../assets/img/logo.png") no-repeat center center/40px;
}
.logo:hover {
  cursor: pointer;
}
.wb {
  position: relative;
  top: -100vh;
  height: 6.5%;
}
.wb:hover {
  cursor: pointer;
}
.user{
  position: relative;
  bottom: 22%;
  height: 6.5%;
}
.user:hover {
  cursor: pointer;
}
.icon {
  width: 50px;
  height: 100%;
}
</style>