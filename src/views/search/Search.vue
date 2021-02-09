<template>
  <div id="search" ref="wrapper">
    <div class="searchnav">
      <div class="searchbox">
        <input
          type="text"
          v-model="value"
          :placeholder="placeHolder"
          @keydown.enter="searchHandler"
          @keyup="searchHandler"
          autofocus="autofocus"
        />
        <span @click="searchback" class="searchback">取消</span>
      </div>
    </div>
    <Scroll :probeType="3" class="content" ref="scroll">
      <SearchHot
        v-if="isShow1"
        :tagList="tagList"
        @tagSearch="tagSearch"
      ></SearchHot>
      <div v-if="isShow2">
        <div v-if="isShow3" class="searchHead" @click="AllClick">
          <img src="~assets/img/bo.png" alt="" />
          <h4>播放全部</h4>
        </div>
        <ul v-for="item in searchResList" :key="item.id" class="searchlist">
          <li class="searchListItem">
            <div class="searchinfo" @click="ListItemClick(item)">
              <div class="songtitle">{{ item.name }}</div>
              <div class="songdetail">
                {{ item.artists[0].name }} - {{ item.album.name }}
              </div>
            </div>
            <span class="more"
              ><img src="~assets/img/more.png" alt="" @click="showShareClick"
            /></span>
          </li>
        </ul>
      </div>
      <!-- 分享弹出层 -->
    <van-popup v-model="show" round position="bottom" :style="{ height: '40%' }" >
      <div class="morePopup">
      <div><img src="~assets/img/Popup/like.png" alt="">收藏歌单</div>
      <div><img src="~assets/img/Popup/download.png" alt="">下载</div>
      <div><img src="~assets/img/Popup/comment.png" alt="">评论（4999）</div>
      <div><img src="~assets/img/Popup/share.png" alt="">分享</div>
      <div><img src="~assets/img/Popup/shut.png" alt="">屏蔽歌曲</div>
      </div>
    </van-popup>
      <div class="hight"></div>
    </Scroll>
  </div>
</template>

<script>
import {
  getSearchSong,
  getSearchHot,
  getSearchDefault,
  getSearchSuggest,
} from "network/search";
import { getSongDetail, getSongUrl } from "network/api";
import { Search, Popup } from "vant";
import SearchHot from "./SearchHot";
import Scroll from "components/common/Scroll";

export default {
  name: "Search",
  components: { [Search.name]: Search, [Popup.name]: Popup, SearchHot, Scroll },

  data() {
    return {
      show: false,
      isShow1: true,
      isShow2: true,
      isShow3: false,
      value: "",
      searchResList: [],
      tagList: [],
      placeHolder: "",
    };
  },
  async created() {
    this.searchDefault();
    this.initSearchHot();
  },
  mounted() {
    this.$nextTick(() => {
      this.$refs.scroll.scroll.refresh();
    });
  },
  methods: {
    searchback() {
      this.$router.back();
      // this.$router.push('/search');
    },
    //关键词提示
    async searchSuggest() {
      const { data: res } = await getSearchSuggest(this.value.trim());
    },
    //搜索默认
    async searchDefault() {
      const { data: res } = await getSearchDefault();
      // console.log(res.data.realkeyword);
      this.placeHolder = res.data.realkeyword;
    },
    //播放全部
    AllClick() {
      this.$message("未开发~");
    },
    //点击更多
    showShareClick() {
      this.show = true;
    },
    iconClick() {
      this.$message("未开发");
    },

    //监听搜索输入
    async searchHandler() {
      if (this.value) {
        const {
          data: { result: list },
        } = await getSearchSong(this.value.trim()).catch((err) => err);
        this.searchResList = list.songs;
        this.isShow1 = false;
        this.isShow2 = true;
        this.isShow3 = true;
      } else {
        const {
          data: { result: list },
        } = await getSearchSong(this.placeHolder.trim()).catch((err) => err);
        this.searchResList = list.songs;
        this.isShow1 = true;
        this.isShow2 = false;
        this.isShow3 = false;
      }
    },
    // 点击列表
    async ListItemClick(item) {
      this.$store.commit("play");
      const {
        data: { songs: res },
      } = await getSongDetail(item.id);
      const { data: url } = await getSongUrl(item.id);
      let currentPlay = {};
      currentPlay.url = url.data[0].url;
      currentPlay.id = item.id;
      currentPlay.singer = item.artists[0].name;
      currentPlay.albumPic = res[0].al.picUrl;
      currentPlay.name = item.name;
      this.$store.commit("addToCurrentPlay", currentPlay);
      this.$store.dispatch("AddToPlayList", currentPlay);
    },

    //热门搜索
    async initSearchHot() {
      const { data: result } = await getSearchHot();
      this.tagList = result.result.hots;
      // console.log(this.tagList);
    },
    tagSearch(item) {
      // console.log(item);
      this.value = item;
      this.searchHandler(this.value);
    },
  },
  watch: {
    "$store.state.currentPlay": function() {},
    value(newVal, oldVal) {
      // console.log(newVal);
      if (newVal === "") {
        this.isShow = false;
      } else {
        this.searchSuggest();
      }
    },
  },
};
</script>

<style scoped>
.searchnav {
  display: flex;
  justify-content: space-around;
  align-items: center;
  text-align: center;
  padding: 2.222vw 0 2.778vw 0;
  border-bottom: 2px solid rgb(230, 230, 230);
}
.searchback {
  flex: 1;
  margin-left: 10px;
  font-size: 17px;
  font-weight: bold;
  color: #64d09c;
}
.searchback img {
  width: 24px;
  height: 24px;
}

.searchbox {
  flex: 7;
}
.searchbox input {
  width: 250px;
  height: 15px;
  background-color: #f7f7f7;
  border: 0px solid;
  outline: none;
  border-radius: 15px;
  background-image: url(~assets/img/navbar/search.png);
  background-size: 20px 20px;
  background-repeat: no-repeat;
  background-position: 10px 5px;
  padding: 8px 10px 8px 40px;
}
.searchHead {
  height: 50px;
  border-bottom: 1px solid rgb(230, 230, 230);
  padding-left: 10px;
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
.searchHead img {
  width: 30px;
  height: 30px;
}
.searchHead h4 {
  width: 100px;
  height: 30px;
  line-height: 30px;
  padding-left: 10px;
  padding-top: 4px;
}
.searchlist {
  padding: 5px 0;
  width: 100%;
}
.searchListItem {
  display: flex;
  width: 95%;
  justify-content: space-between;
  align-items: center;
  margin: 5px auto;
  padding-bottom: 5px;
  border-bottom: 1px solid rgb(230, 230, 230);
}
.searchinfo {
  margin-left: 5px;
  width: 90%;
}
.songtitle {
  font-size: 4.167vw;
  margin-bottom: 4px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  max-width: 280px;
}
.songdetail {
  display: inline-block;
  font-size: 3.333vw;
  opacity: 0.7;
  color: #707070;
}
.hight {
  height: 1200px;
}
.more {
  margin-right: -5px;
}
#search {
  height: 100vh;
}
.content {
  height: calc(100% - 49px);
  overflow: hidden;
  position: absolute;
  top: 49px;
  bottom: 0px;
  left: 0;
  right: 0;
}
.playernavbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: white;
  background-image: radial-gradient(
    43% 116% at bottom center,
    #535353 5%,
    #464646 18%,
    rgb(27, 26, 26) 70%
  );
}
.playerback {
  /* flex: 1.5; */
  margin-left: 20px;
}
.playersongtitle {
  /* flex: 5; */
  text-align: start;
  display: flex;
  flex-direction: column;
  font-size: 4.444vw;
  line-height: 6.944vw;
  align-items: baseline;
  border-bottom: 0.8px solid rgba(49, 47, 47, 0.8);
  letter-spacing: 1.5px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  margin-left: -100px;
}
.playersongtitle span:nth-child(1) {
  margin-top: 1.389vw;
}
.playersongtitle span:nth-child(2) {
  font-size: 3.333vw;
  opacity: 0.7;
  margin-bottom: 2px;
}
.playershare {
  /* flex: 1.5; */
  margin-right: 20px;
}
.playershare img {
  height: 28px;
  width: 28px;
}

/* morePopup弹出层 */
.morePopup {
  display: flex;
  flex-flow: column;
  justify-content: space-evenly;
  margin-top: 15px;
  margin-left: 25px;
}

.morePopup div {
  height: 50px;
  width: 100%;
  display: flex;
  justify-content: start;
  align-items: center;
}
.morePopup img {
  
  padding-right: 10px;
}
</style>
