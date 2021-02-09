<template>
  <div class="nav-bar">
    <div class="left"><slot name="left"></slot></div>
    <div class="center"><slot name="center"></slot></div>
    <div class="right"><slot name="right"></slot></div>
  </div>
</template>

<script>
export default {
  name: "NavBar",
  data() {
    return {};
  },
  components: {},
};
</script>

<style scoped>
.nav-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  line-height: 49px;
  height: 49px;
  text-align: center;
  box-shadow: 0 1px 1px rgba(100, 100, 100, 0.1);
}


.left {
  width: 32px;
  height: 32px;
  margin-left: 20px;
}
.right {
  width: 80px;
  height: 32px;
  margin-right: 15px;
}

.center {
  padding-left: 40px;
}
</style>
