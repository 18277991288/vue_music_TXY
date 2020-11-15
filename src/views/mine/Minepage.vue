<template>
  <div class="minepage">
    <van-tabs v-model="active"  
    background="rgb(245, 246, 247)" 
    sticky offset-top="45px" >
      <van-tab title="创建歌单"
        >
        <div class="back"><ul>
          <li>1</li>
          <li>1</li>
          <li>1</li>
          <li>1</li>
          <li>1</li>
          <li>1</li>
          <li>1</li>
          <li>1</li>
          <li>1</li>
          <li>1</li>
          <li>1</li>
          <li>1</li>
          <li>1</li>
        </ul></div>
        </van-tab
      >
      <van-tab title="收藏歌单">
        <div class="back"><ul>
          <li>2</li>
          <li>2</li>
          <li>2</li>
          <li>2</li>
          <li>2</li>
          <li>2</li>
          <li>2</li>
          <li>2</li>
          <li>2</li>
          <li>2</li>
          <li>2</li>
          <li>2</li>
          <li>2</li>
          <li>2</li>
          <li>2</li>
          <li>2</li>
        </ul></div>
        
      </van-tab>
      <van-tab title="歌单助手">
        <div class="back"><ul>
          <li>3</li>
          <li>3</li>
          <li>3</li>
          <li>3</li>
          <li>3</li>
          <li>3</li>
          <li>3</li>
          <li>3</li>
          <li>3</li>
          <li>3</li>
          <li>3</li>
          <li>3</li>
          <li>3</li>
          <li>3</li>
          <li>3</li>
          <li>3</li>
        </ul></div>
        
      </van-tab>
    </van-tabs>
  </div>
</template>

<script>
import Vue from "vue";
import { Tab, Tabs } from "vant";

Vue.use(Tab);
Vue.use(Tabs);
export default {
  name: "Minepage",
  components: {},
  data() {
    return {
      active: 3,
    };
  },
};
</script>

<style scoped>
.back {
  width: 90%;
  height: 1000px;
  background-color: #fff;
  margin: 10px auto;
  border-radius: 15px;
}
</style>
