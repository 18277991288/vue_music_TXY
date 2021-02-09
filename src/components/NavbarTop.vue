<template>
  <!-- nav上层 -->
  
  <div>
    <nav-bar class="home-nav">
      <div slot="left">
        <img src="~assets/img/navbar/menu.png" alt="" @click="showPopup" />
          <van-popup v-model="show" position="left" closeable class="menusPopup">
        <div class="avatar"></div>
        <div class="mygit" @click="gitClick">
          <img src="~assets/img/github.png" alt="" />
          <span>github(点击进入主页)</span>
        </div>
        <div class="mygit" >
          <img src="~assets/img/wechat.png" alt="" />
          <span>Yu_2609813922</span>
        </div>
        <div class="mygit" >
          <img src="~assets/img/phone.png" alt="" />
          <span>19522968814</span>
        </div>
      </van-popup>
      </div>
      <div slot="center" class="home-center"><h3>music</h3></div>
      <div slot="right" class="home-right">
        <img src="~assets/img/navbar/search.png" alt="" @click="searchClick" />
      </div>
    </nav-bar>
  </div>
</template>

<script>
import NavBar from "components/common/NavBar";
import { Popup } from "vant";


export default {
  name: "NavbarTop",
  components: {
    [Popup.name]: Popup,
    NavBar,
  },
  methods: {
    searchClick() {
      this.$router.push("/search");
    },
    //侧边栏
    menusClick() {
      this.$store.commit("openMenus");
    },
    showPopup() {
      this.show = true;
      
    },
    //github
    gitClick() {
      // window.open("https://github.com/rt442979559/cloudMusic")
      window.open("https://github.com/18277991288/wyymusic/tree/main");
    },
  },
  data() {
    return {
      show: false,
    };
  },
};
</script>

<style scoped>
.menusPopup {
  z-index: 1001;
  background-color: white;
}
/* navbar上层 */
.home-nav {
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 999;
  background: #fff;
}
.home-nav img {
  height: 28px;
  width: 28px;
}
.home-right img {
  height: 25px;
  width: 25px;
  margin-left: 40px;
}
.home-center {
  color: rgb(100, 208, 156);
  font-size: 17px;
}

/* 弹出层 */
.menusPopup {
  height: 100vh;
  width: 80vw;
}
.avatar {
  width: 100%;
  height: 30vh;
  background: url(~assets/img/yu.jpg) no-repeat;
  background-size: 100%;
  background-position: 50%;
}
.avatar img {
  height: 100%;
  width: 100%;
}
.mygit {
  height: 10vh;
  line-height: 10vh;
  opacity: 0.8;
}
.mygit img {
  margin: 0 6vw -10px -2.5vh;
  margin-right: 10px;
}
</style>
