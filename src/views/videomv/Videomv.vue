<template>
  <div id="Home" class="wrapper" ref="wrapper">
    <Scroll :probeType="3" class="content" ref="scroll">
      <van-pull-refresh
        v-model="isLoading"
        @refresh="onRefresh"
        success-text="刷新成功"
      >
        <div id="VideoBody">
          <div class="VideoBodyTop">
            <div><p>Mv</p></div>
          </div>
          <div class="middle">
            <div
              class="MvList"
              v-for="(item,index) in MvList"
              :key="item.id"
              @click="showPopup(index)"
            >
              <div class="photo">
                <div class="mid">
                  <img :src="item.picUrl" alt="" />
                </div>
              </div>
              <div class="text">{{ item.name }}</div>
              <div class="low">
                <img src="../../assets/img/play.png" alt="" />
                <p>{{ item.playCount | playCount }}</p>
              </div>
            </div>
          </div>
        </div>
      </van-pull-refresh> 
      <div class="kong"></div>
    </Scroll>
    <van-popup
      v-model="show"
      position="left"
      closeable
      class="popup"
      @close="ClosePopup"
      @opened="OpenedPopup"
    >
      <div class="PopupText">MV</div>
      <div class="video" @click="VideoClick">
        <video
          width="400"
          height="250"
          autoplay="autoplay"
          ref="MiniPlayer"
          :src="video_url"
        ></video>
        <div v-show="this.isPaused" class="paused">
          <img src="~assets/img/play1.png" alt="" />
        </div>
      </div>
      <div class="gongneng">
        <img src="~assets/img/video/like.png" alt="" />
        <img src="~assets/img/video/say.png" alt="" />
        <img src="~assets/img/video/left.png" alt="" />
        <img src="~assets/img/video/save.png" alt="" />
      </div>
    </van-popup>
  </div>
</template>

<script>
// import VideoBody from './VideoBody.vue';
import Scroll from "components/common/Scroll";
import { PullRefresh } from "vant";
import { getPersonalized } from "network/api";
import { Popup } from "vant";

export default {
  name: "Home",
  components: {
    Scroll,
    // VideoBody,
    [PullRefresh.name]: PullRefresh,
    [Popup.name]: Popup,
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
      isLoading: false,
      MvList: [],
      show: false,
      isPaused: false,
      video_url:"",  
    };
  },
  async created() {
    const {
      data: { result: res },
    } = await getPersonalized();
    this.MvList = res;
  },
  filters: {
    playCount(value) {
      return (value / 10000).toFixed(0) + "万";
    },
  },
  methods: {
    onRefresh() {
      setTimeout(() => {
        this.isLoading = false;
        // console.log(this.count);
        if (this.count < 9) {
          this.count++;
          // this.$refs.personalized.getPersonalized(this.count * 6,(this.count + 1) * 6);
        } else {
          this.count = 0;
          // this.$refs.personalized.getPersonalized(this.count * 6,(this.count + 1) * 6);
        }
        this.initScroll();
      }, 1000);
    },
    initScroll() {
      this.$nextTick(() => {
        this.$refs.scroll.scroll.refresh();
      });
    },
    showPopup(i) {
      switch (i) {
          case 0:
            this.video_url = "http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4";
            this.show = true;
          break;
          case 1:
            this.video_url = "http://vjs.zencdn.net/v/oceans.mp4";
            this.show = true;
          break;
          case 2:
            this.video_url = "https://media.w3.org/2010/05/sintel/trailer.mp4";
            this.show = true;
          break;
          case 3:
            this.video_url = "https://v-cdn.zjol.com.cn/280443.mp4";
            this.show = true;
          break;
          case 4:
            this.video_url = "https://v-cdn.zjol.com.cn/276982.mp4";
            this.show = true;
          break;
          case 5:
            this.video_url = "https://v-cdn.zjol.com.cn/276984.mp4";
            this.show = true;
          break;
          case 6:
            this.video_url = "https://v-cdn.zjol.com.cn/276985.mp4";
            this.show = true;
          break;
          case 7:
            this.video_url = "https://v-cdn.zjol.com.cn/276986.mp4";
            this.show = true;
          break;
          case 8:
            this.video_url = "https://v-cdn.zjol.com.cn/276987.mp4";
            this.show = true;
          break;
          case 9:
            this.video_url = "https://v-cdn.zjol.com.cn/276988.mp4";
            this.show = true;
          break;
          case 10:
            this.video_url = "https://v-cdn.zjol.com.cn/276989.mp4";
            this.show = true;
          break;
          case 11:
            this.video_url = "https://v-cdn.zjol.com.cn/276990.mp4";
            this.show = true;
          break;
          case 12:
            this.video_url = "https://v-cdn.zjol.com.cn/276991.mp4";
            this.show = true;
          break;
          case 13:
            this.video_url = "https://v-cdn.zjol.com.cn/276992.mp4";
            this.show = true;
          break;
          case 14:
            this.video_url = "https://v-cdn.zjol.com.cn/276993.mp4";
            this.show = true;
          break;
          case 15:
            this.video_url = "https://v-cdn.zjol.com.cn/276994.mp4";
            this.show = true;
          break;
          case 16:
            this.video_url = "https://v-cdn.zjol.com.cn/276995.mp4";
            this.show = true;
          break;
          case 17:
            this.video_url = "https://v-cdn.zjol.com.cn/276996.mp4";
            this.show = true;
          break;
          case 18:
            this.video_url = "https://v-cdn.zjol.com.cn/276997.mp4";
            this.show = true;
          break;
        }
      
    },
    OpenedPopup() {
      this.$refs.MiniPlayer.play();
      this.isPaused = false;
    },
    ClosePopup() {
      this.$refs.MiniPlayer.pause();
      this.isPaused = true;
    },

    VideoClick() {
      if (this.$refs.MiniPlayer.paused == false) {
        this.$refs.MiniPlayer.pause();
        this.isPaused = true;
      } else {
        this.$refs.MiniPlayer.play();
        this.isPaused = false;
      }
    },
  },
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
  top: 49px;
  bottom: 0px;
  left: 0;
  right: 0;
  overflow: hidden;
}
.kong {
  height: 50px;
}
.VideoBodyTop {
  width: 100%;
  height: 30px;
  margin-top: 10px;
}
.VideoBodyTop div {
  width: 70px;
  height: 30px;
  background-color: #caebdb;
  margin: 0 auto;
  border-radius: 20px;
}
.VideoBodyTop p {
  width: 25px;
  line-height: 30px;
  margin: 0 auto;
  color: #64d09c;
}

.middle {
  width: 100%;
  background-color: #fff;
  padding-top: 15px;
  display: flex;
  justify-content: space-evenly;
  flex-flow: wrap;
  align-content: start;
}

.MvList {
  width: 45%;
  height: 250px;
  background-color: #fff;
  margin-bottom: 14px;
  border-radius: 15px;
  box-shadow: 1px 1px 2px #ccc;
  overflow: hidden;
}
.photo {
  background-color: rgba(0, 0, 0, 0.2);
  height: 190px;
  border-top-left-radius: 15px;
  border-top-right-radius: 15px;
  position: relative;
}

.mid {
  overflow: hidden;
}
.mid img {
  width: 169px;
  height: 189px;
}
.text {
  width: 150px;
  height: 30px;
  font-size: 14px;
  margin-left: 10px;
  line-height: 30px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.low {
  width: 150px;
  height: 30px;
  font-size: 14px;
  margin-left: 10px;
  margin-top: 10px;
  line-height: 30px;
  color: #ccc;
  position: relative;
}
.low img {
  position: absolute;
  top: 2px;
  width: 16px;
  height: 16px;
}
.low p {
  position: absolute;
  top: -18px;
  left: 20px;
}

.popup {
  width: 100%;
  height: 100%;
  background-color: #010101;
}
.PopupText {
  color: #010101;
  width: 45px;
  height: 30px;
  margin: 30px auto;
  text-align: center;
  line-height: 30px;
  background-color: #ccc;
  border-radius: 15px;
  /* font-weight: 700; */
}
.video {
  width: 100%;
  height: 250px;
  /* background-color: #fff; */
  margin-top: 120px;
  position: relative;
}
.paused {
  width: 64px;
  height: 64px;
  position: absolute;
  top: 90px;
  left: 160px;
}
.gongneng {
  width: 50px;
  height: 250px;
  margin-left: 315px;
  margin-top: -35px;
  display: flex;
  flex-flow: column;
  justify-content: space-evenly;
  align-items: center;
}
.gongneng img {
  width: 32px;
  height: 32px;
}
</style>
