<template>
  <!-- 最新音乐 -->
  <div class="newsong">
    <div class="recommend">
      <div class="recommendmore" >最新音乐</div>
      <div class="recommendbtn" @click="newsongClick">查看更多</div>
    </div>

    <NewSong id="NewSong"></NewSong>
  </div>
</template>

<script>
import NewSong from "components/common/NewSong";
export default {
  components: { NewSong },
  methods: {
    newsongClick(){
      this.$message('未开发~');
    }
  }
};
</script>

<style scoped>
.newsong {
  margin-top: 2.778vw;
}
.personalizednewsong {
  /* margin: 2.333vw 0 0 0px; */
  font-size: 3.889vw;
  border-left: 0.417vw solid red;
  padding: 0 0 0 1.667vw;
}
#NewSong{
  margin-top: -1.667vw;
}
.recommend {
  display: flex;
  justify-content: space-between;
  border-top: 1px solid #f0f0f0;
  
}
.recommendmore {
  font-size: 3.889vw;
  margin: 10px 0 0 0px;
  font-size: 3.889vw;
  border-left: 2px solid #64d09c;
  padding: 5px 0 0 1.667vw;
}
.recommendbtn {
  font-size: 14px;
  height: 25px;
  width: 80px;
  text-align: center;
  line-height: 25px;
  margin-right: 10px;
  margin-top: 10px;
  border: 1px solid #d1d0d0;
  border-radius: 20px;
}
</style>