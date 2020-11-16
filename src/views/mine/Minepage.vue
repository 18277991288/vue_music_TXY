<template>
  <div class="minepage">
    <van-tabs
      v-model="active"
      background="rgb(245, 246, 247)"
      sticky
      offset-top="45px"
    >
      <van-tab title="创建歌单">
        <div class="back">
          <div class="creat">
            <div class="creatleft">创建歌单（8个）</div>
            <div class="creatright">
              <div><img src="~assets/img/jia.png" alt="" /></div>
              <div @click="showPopup">
                <img src="~assets/img/more1.png" alt="" />
              </div>
            </div>
          </div>

          <van-popup v-model="show" position="bottom" class="sortPopup" round>
            <div class="sortname">创建歌单（8个）</div>
            <div>
              <img src="~assets/img/1.png" alt="" /><span>新建歌单</span>
            </div>
            <div>
              <img src="~assets/img/2.png" alt="" /><span>管理歌单</span>
            </div>
            <div>
              <img src="~assets/img/3.png" alt="" /><span
                >导入外部歌单</span
              >
            </div>
            <div>
              <img src="~assets/img/4.png" alt="" /><span>恢复歌单</span>
            </div>
          </van-popup>

          <ul>
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
          </ul>
        </div>
      </van-tab>
      <van-tab title="收藏歌单">
        <div class="back">
          <ul>
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
          </ul>
        </div>
      </van-tab>
      <van-tab title="歌单助手">
        <div class="back">
          <ul>
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
          </ul>
        </div>
      </van-tab>
    </van-tabs>
  </div>
</template>

<script>
import Vue from "vue";
import { Tab, Tabs } from "vant";
import { Popup } from "vant";

Vue.use(Popup);
Vue.use(Tab);
Vue.use(Tabs);
export default {
  name: "Minepage",
  components: {},
  data() {
    return {
      active: 3,
      show: false,
    };
  },
  methods: {
    showPopup() {
      this.show = true;
    },
  },
};
</script>

<style scoped>
.back {
  width: 90%;
  
  background-color: #fff;
  margin: 10px auto;
  border-radius: 15px;
}
.creat {
  display: flex;
  justify-content: space-between;
}
.creatleft {
  height: 40px;
  width: 120px;
  text-align: center;
  line-height: 40px;
  font-size: 8px;
  color: rgb(88, 86, 86);
}
.creatright {
  height: 40px;
  width: 100px;
  display: flex;
  justify-content: space-around;
}
.creatright div {
  width: 40px;
  height: 40px;
  text-align: center;
  line-height: 40px;
}
.sortPopup {
  height: 200px;
  display: flex;
  flex-flow: column;
  justify-content: space-evenly;
}
.sortPopup div {
  margin-left: 20px;
  display: flex;
  align-items: center;
}

</style>
