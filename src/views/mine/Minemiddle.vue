<template>
  <div class="minemiddle">
    <ul class="flex1">
      <li><img src="../../assets/img/minemiddle/1.png" alt="" /><p>本地音乐</p></li>
      <li><img src="../../assets/img/minemiddle/2.png" alt="" /><p>云盘</p></li>
      <li><img src="../../assets/img/minemiddle/3.png" alt="" /><p>已购</p></li>
      <li><img src="../../assets/img/minemiddle/4.png" alt="" /><p>最近播放</p></li>
     </ul> 
      <ul class="flex2">
      <li><img src="../../assets/img/minemiddle/5.png" alt="" /><p>我的好友</p></li>
      <li><img src="../../assets/img/minemiddle/6.png" alt="" /><p>收藏和赞</p></li>
      <li><img src="../../assets/img/minemiddle/7.png" alt="" /><p>我的电台</p></li>
      <li><img src="../../assets/img/minemiddle/8.png" alt="" /><p>音乐应用</p></li>
    </ul> 
  </div>
</template>

<script>
export default {
  name: "Minemiddle",
  components: {},
  data() {
    return {};
  },
};
</script>

<style scoped>
.minemiddle {
  width: 90%;
  height: 200px;
  background-color: #fff;
  margin: 10px auto;
  border-radius: 15px;
}
.flex1 {
  display: flex;
  justify-content: space-between;
  
}
.flex2{
  display: flex;
  justify-content: space-between;
}
.minemiddle ul li {
  float: left;
  width: 80px;
  height: 80px;
  padding: 10px 0;
}
.minemiddle ul li img {
  width: 40px;
  height: 40px;
  margin-top: 15px;
  margin-left: 20px;
}
.minemiddle ul li p {
  font-size: 14px;
  margin-top: 3px;
  margin-left: -2px;
  text-align: center;
}


</style>
