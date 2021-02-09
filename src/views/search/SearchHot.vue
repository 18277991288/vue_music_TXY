<template>
  <div>
    <div class="kong"></div>
    <!-- <div class="up"><img src="../../assets/img/2020.jpg" alt=""></div> -->
    <div class="title">
      <span>热搜榜</span>
    </div>
    <div class="searchhot">
      <ol class="hot">
        <li v-for="item in tagList" :key="item.first" @click="tagClick(item)">
          {{ item.first }} <img src="~assets/img/HOT1.png" alt="" />
        </li>
      </ol>
    </div>
  </div>
</template>

<script>
import { Tag } from "vant";
export default {
  name: "SearchHot",
  components: { [Tag.name]: Tag },
  props: ["tagList"],
  methods: {
    tagClick(item) {
      this.$emit("tagSearch", item.first);
    },
  },
};
</script>

<style scoped>
.title {
  margin: 10px auto;
  padding-left: 10px;
  width: 85%;
  height: 30px;
  border-bottom: 2px solid  #64d09c;
  font-size: 15px;
  font-weight: 900;
  color: #64d09c;
}
.up {
  
}
.up img {
  width: 100%;
  height: 150px;
}

.searchhot {
  width: 300px;
  height: 300px;
  margin: 30px auto;
}

.searchhot ol {
  width: 300px;
  height: 300px;
  display: flex;
  flex-flow: row wrap;
  justify-content: space-around;
  align-content: flex-start;
}
.searchhot ol li {
  position: relative;
  width: 140px;
  height: 30px;
  /* background-color: pink; */
  margin-bottom: 10px;
  margin-left: 10px;
  font-weight: 700;
  font-size: 15px;
  list-style: decimal;

}
.searchhot ol li img {
  position: absolute;
  top: 0px;
  margin-left: 5px;
  
}

.hot li:nth-child(n + 5) img{
  display: none;
}
.hot img {
  /* width: 50px;
  height: 50px; */
}
.kong {
  height: 10px;
}
</style>