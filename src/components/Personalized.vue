<template>
  <!-- 推荐歌单 -->
  <div class="personalized">
    <div class="recommend">
      <div class="recommendmore" >推荐歌单</div>
      <div class="recommendbtn" @click="recommendClick">查看更多</div>
    </div>

    <div class="playcard" v-if="list.length">
      <PlayCard
        v-for="item in list"
        :desc="item.copywriter"
        :id="item.id"
        :img="item.picUrl"
        :key="item.id"
        :name="item.name"
        :playcount="item.playCount"
      ></PlayCard>
    </div>
  </div>
</template>

<script>
import { getPersonalized } from "network/api";
import PlayCard from "./common/PlayCard";
export default {
  name: "Personalized",
  components: { PlayCard },
  async created() {
    this.getPersonalized(0, 6);
  },
  data() {
    return {
      list: [],
    };
  },
  methods: {
    async getPersonalized(a, b) {
      //只获取6组数据进行 渲染展示
      const { data: res } = await getPersonalized({ limit: 60 });
      this.list = res.result.slice(a, b);
      // console.log(res);
    },
    recommendClick() {
      this.$router.push('/songcate')
      this.$store.commit('changeTabIndex',1)
    },
  },
};
</script>

<style scoped>
.playcard {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}
.recommend {
  display: flex;
  justify-content: space-between;
  
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
