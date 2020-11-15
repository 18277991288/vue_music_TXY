<template>
  <div class="minelike">
    <div class="minelike-icon"><img src="~assets/img/minemiddle/9.png" alt=""></div>
    <div class="msg">
      <p>我喜欢的音乐</p>
      <span>已下载9首</span>
      </div>
    <div class="xindong">心动模式</div>
  </div>
</template>

<script>
export default {
  name: "Minelike",
  components: {},
  data() {
    return {};
  },
};
</script>

<style scoped>
.minelike {
  width: 90%;
  height: 75px;
  background-color: #fff;
  margin: 20px auto;
  border-radius: 15px;
}
.minelike-icon {
  float: left;
  background: pink;
  height: 50px;
  width: 50px;
  margin: 13px 20px;
  border-radius: 10px;
}
.minelike-icon img {
  margin: 10px 9px;
}
.msg {
  float: left;
}
.msg span {
  font-size: 10px;
  
}
.xindong {
  float: right;
  margin: 25px 20px;;
  height: 20px;
  width: 80px;
  font-size: 10px;
  border-radius: 15px;
  border: 1px solid rgb(221, 221, 221);
  text-align: center;
  line-height: 20px;
}
</style>
