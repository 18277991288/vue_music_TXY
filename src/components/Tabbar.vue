<template>
  <!-- tabbar上层 -->
  <div class="tabbar">
    <div class="tabbarTop">
      <div class="tabbaricon">
        <div
          class="tabbar-home"
          @click="tabhomeClick(0)"
          :class="currentIndex == 0 ? '' : 'inactive'"
        >
          <img src="~assets/img/tabbar/music-active.png" alt />
        </div>
        <div
          class="tabbar-videomv"
          @click="tabvideomvClick(1)"
          :class="currentIndex == 1 ? '' : 'inactive'"
        >
          <img src="~assets/img/tabbar/video-active.png" alt />
        </div>
        <div
          class="tabbar-videomv"
          @click="tabplazaClick(2)"
          :class="currentIndex == 2 ? '' : 'inactive'"
        >
          <img src="~assets/img/tabbar/plaza-active.png" alt />
        </div>
        <div
          class="tabbar-mine"
          @click="tabmineClick(3)"
          :class="currentIndex == 3 ? '' : 'inactive'"
        >
          <img src="~assets/img/tabbar/profile-active.png" alt />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TabbarTop",
  components: {},
  methods: {
    tabmineClick(index) {
      this.$router.push("/mine");
      this.currentIndex = index;
    },
    tabhomeClick(index) {
      this.$router.push("/index");
      this.$store.commit("changeTabIndex", 0);
      this.currentIndex = index;
    },
    tabvideomvClick(index) {
      this.$router.push('/videomv');
      this.currentIndex = index;
    },
    tabplazaClick(index) {
      this.$router.push('/plaza');
      this.currentIndex = index;
    },
  },
  data() {
    return {
      currentIndex: 0,
    };
  },
};
</script>

<style scoped>
/* tabbar上层 */
.tabbarTop {
  height: 48px;
  text-align: center;
  line-height: 45px;
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: #f6f6f6;
  width: 100%;
  z-index: 888;
}

/* 中间icon区 */
.tabbaricon {
  width: 100%;
  background-color: #f6f6f6;
  /* transform: translate(50%); */
  display: flex;
  justify-content: space-evenly;
  align-items: center;
}
img {
  width: 7.222vw;
  vertical-align: middle;
}
.tabbar-mine {
  background-color: #f6f6f6;
}
.tabbar-home {
  background-color: #f6f6f6;
}
.tabbar-videomv {
  background-color: #f6f6f6;
}
.inactive {
  opacity: 0.3;
}
</style>
