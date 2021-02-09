<template>
  <div id="Home" class="wrapper" ref="wrapper">
    <Scroll :probeType="3" class="content" ref="scroll" >
    <van-pull-refresh v-model="isLoading" @refresh="onRefresh" success-text="刷新成功">
      <Banners></Banners>
      <Recommend></Recommend>
      <Personalized ref="personalized"></Personalized>
      <PersonalizedNewSong></PersonalizedNewSong>
      <PersonalizedExclusive></PersonalizedExclusive>
      <PersonalizedMv></PersonalizedMv>
    </van-pull-refresh>
    <div class="kong"></div>
    </Scroll>
  </div>
</template>

<script>
import Banners from "components/Banners";
import NavbarBtm from "components/NavbarBtm";
import Recommend from "components/Recommend";
import Personalized from "components/Personalized";
import PersonalizedNewSong from "components/PersonalizedNewSong";
import PersonalizedExclusive from "components/PersonalizedExclusive";
import PersonalizedMv from "components/PersonalizedMv";
import Scroll from "components/common/Scroll";
import { PullRefresh } from "vant";  
export default {
  name: "Home", 
  components: {
    Banners,
    NavbarBtm,
    Recommend,
    Personalized,
    PersonalizedNewSong,
    PersonalizedExclusive,
    PersonalizedMv,
    Scroll,
    [PullRefresh.name]: PullRefresh
  },
  mounted() {
    this.initScroll();
  },
  activated() {
    this.initScroll();
  },
  data() {
    return {
      count: 0,
      isLoading: false
    };
  },
  methods: {
    onRefresh() {
      setTimeout(() => {
        this.isLoading = false;
        // console.log(this.count);
        if (this.count < 9) {
          this.count++;
          this.$refs.personalized.getPersonalized(this.count * 6,(this.count + 1) * 6);
        } else {
          this.count = 0;
          this.$refs.personalized.getPersonalized(this.count * 6,(this.count + 1) * 6);
        }
        this.initScroll();
      }, 1000);
    },
    initScroll() {
      this.$nextTick(() => {
        this.$refs.scroll.scroll.refresh();
      });
    },
  }
};
</script>

<style scoped>
#home {
  position: relative;
  overflow: hidden;
}
.content {
  height: calc(100vh - 90px);
  overflow: hidden;
  position: absolute;
  top: 90px;
  bottom: 0px;
  left: 0;
  right: 0;
  overflow: hidden;
}
.kong {
  height: 100px;
}
</style>