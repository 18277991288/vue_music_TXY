<template>
  <div id="Home" class="wrapper" ref="wrapper">
    <div class="PlazaTop">音乐广场</div>
    <Scroll :probeType="3" class="content" ref="scroll">
      <van-pull-refresh
        v-model="isLoading"
        @refresh="onRefresh"
        success-text="刷新成功"
      >
    
      <div class="list" v-if="addShow">
      <div class="photo"><img src="~assets/img/plaza/yu.jpg" alt="" /></div>
      <div class="name">陶星宇</div>
      <div class="text">
        {{ message }}
      </div>
      <div class="pic" >
        <img :src="index.content" alt="" v-for="(index,id) in fileList" :key="id"/>
      </div>
      <div class="more" @click="ShowMore(4)">
        <img src="~assets/img/plaza/more.png" alt="" />
      </div>
      <div class="like" v-show="this.ShowLike4" @click="ShowMore(4)">
        <div>
          <img src="~assets/img/plaza/like.png" alt="" /><span>赞</span>
        </div>
        <div>
          <img src="~assets/img/plaza/say.png" alt="" /><span>评论</span>
        </div>
      </div> 
    </div>


    <div class="list">
      <div class="photo"><img src="~assets/img/plaza/jie1.png" alt="" /></div>
      <div class="name">Libero-xxxx</div>
      <div class="text" >
        收拾房间看着这一面杰哥的海报墙<br />真的好感慨<br />不知不觉粉了杰哥十几年<br />从五年级到如今大学快毕业<br />一《这就是爱》
      </div>
      <div class="pic">
        <img src="~assets/img/plaza/jie3.png" alt="" />
        <img src="~assets/img/plaza/jie4.png" alt="" />
        <img src="~assets/img/plaza/jie2.png" alt="" />
      </div>
      <div class="more" @click="ShowMore(1)">
        <img src="~assets/img/plaza/more.png" alt="" />
      </div>
      <div class="like" v-show="this.ShowLike1" @click="ShowMore(1)">
        <div>
          <img src="~assets/img/plaza/like.png" alt="" /><span>赞</span>
        </div>
        <div>
          <img src="~assets/img/plaza/say.png" alt="" /><span>评论</span>
        </div>
      </div>
    </div>
    <div class="list">
      <div class="photo"><img src="~assets/img/plaza/lun1.png" alt="" /></div>
      <div class="name">等四季断流</div>
      <div class="text">
        #周杰伦#<br />#周杰伦上春晚#<br />杰迷朋友们喜欢杰伦几年了<br />哪一年开始的。<br />一《稻香》
      </div>
      <div class="pic">
        <img src="~assets/img/plaza/lun4.png" alt="" />
        <img src="~assets/img/plaza/lun2.png" alt="" />
        <img src="~assets/img/plaza/lun3.png" alt="" />
      </div>
      <div class="more" @click="ShowMore(2)">
        <img src="~assets/img/plaza/more.png" alt="" />
      </div>
      <div class="like" v-show="this.ShowLike2" @click="ShowMore(2)">
        <div>
          <img src="~assets/img/plaza/like.png" alt="" /><span>赞</span>
        </div>
        <div>
          <img src="~assets/img/plaza/say.png" alt="" /><span>评论</span>
        </div>
      </div>
    </div>
    <div class="list">
      <div class="photo"><img src="~assets/img/plaza/yang3.png" alt="" /></div>
      <div class="name">深夜小酒屋</div>
      <div class="text">
        #牛年牛牛牛#
        <br />这首歌听上去欢快，但听着听着会有想哭的感觉，这是首用欢快节奏包装的悲伤情歌。<br />一《心乱飞》
      </div>
      <div class="pic">
        <img src="../../assets/img/plaza/yang.png" alt="" />
        <img src="../../assets/img/plaza/yang1.png" alt="" />
        <img src="../../assets/img/plaza/yang2.png" alt="" />
      </div>
      <div class="more" @click="ShowMore(3)">
        <img src="~assets/img/plaza/more.png" alt="" />
      </div>
      <div class="like" v-show="this.ShowLike3" @click="ShowMore(3)">
        <div>
          <img src="~assets/img/plaza/like.png" alt="" /><span>赞</span>
        </div>
        <div>
          <img src="~assets/img/plaza/say.png" alt="" /><span>评论</span>
        </div>
      </div>
    </div>
    <div style="text-align: center;opacity: 0.6;margin-top: 20px;">
      ----没有更多动态了----
    </div>
      </van-pull-refresh>
      <div class="kong"></div>
    </Scroll>
    <div class="add" @click="showPopup">
      <img src="~assets/img/plaza/add.png" alt="" />
    </div>
    <van-popup v-model="show" class="popup" :overlay="false" position="bottom">
      <div class="top">
        <div class="left" @click="cancel">取消</div>
        <div class="right" @click="submit">发表</div>
      </div>
      <form action="">
        <textarea class="Article" v-model="message" placeholder="这一刻的想法..." ></textarea>
        <van-uploader class="uploader" :after-read="afterRead" preview-size="100px" v-model="fileList" :max-count="3"/>
      </form>

    </van-popup>
  </div>
</template>

<script>

import Scroll from "components/common/Scroll";
import { PullRefresh } from "vant";
import { Popup } from "vant";
import { Uploader } from 'vant';

export default {
  name: "Home",
  components: {
    Scroll,
    // PlazaBody,
    [Popup.name]: Popup,
    [Uploader.name]: Uploader,
    [PullRefresh.name]: PullRefresh,
  },
  mounted() {
    this.initScroll();
  },
  activated() {
    this.initScroll();
  },
  data() {
    return {
      isLoading: false,
      show: false,
      fileList: [],//上传图片
      message:"",//文本域内容
      addShow:false,//发布新动态
      ShowLike1: false,
      ShowLike2: false,
      ShowLike3: false,
      ShowLike4: false,
    };
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
     ShowMore(i) {
      this.ShowLike = !this.ShowLike;
      switch (i) {
        case 1:
          this.ShowLike1 = !this.ShowLike1;
          break;
        case 2:
          this.ShowLike2 = !this.ShowLike2;
          break;
        case 3:
          this.ShowLike3 = !this.ShowLike3;
          break;
        case 4:
          this.ShowLike4 = !this.ShowLike4;
          break;
      }
    },
    initScroll() {
      this.$nextTick(() => {
        this.$refs.scroll.scroll.refresh();
      });
    },
    showPopup() {
      this.show = true;
    },
    afterRead(file) {
      // 此时可以自行将文件上传至服务器
    },
    cancel() {
      this.show = false;
      this.message = "" ;
      this.fileList = []

    },
    submit() {
      if (this.message == "") {
        this.$message('您还没有输入内容');
      }else if (this.fileList.length == 0) {
        this.$message('您还没有上传图片');

      }else {
      this.$message('发表成功！');
      this.addShow = true
      this.show = false; 
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
.PlazaTop {
  width: 100%;
  height: 49px;
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 999;
  background: #fff;
  color: rgb(100, 208, 156);
  font-size: 17px;
  align-items: center;
  line-height: 49px;
  box-shadow: 0 1px 1px rgba(100, 100, 100, 0.1);
  text-align: center;
  font-weight: bold;
}
.add {
  width: 50px;
  height: 50px;
  position: fixed;
  bottom: 160px;
  right: 0px;
  z-index: 888;
}
.popup {
  width: 100%;
  height: 100%;
}
.top {
  height: 50px;
  width: 100%;
  line-height: 50px;
  font-size: 18px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.left {
  margin-left: 20px;
}
.right {
  margin-right: 20px;
  height: 35px;
  width: 60px;
  background-color: #57be6a;
  text-align: center;
  line-height: 35px;
  border-radius: 8px;
  color: #fff;
}
.Article {
  width: 85%;
  height: 100px;
  margin-top: 20px;
  margin-left: 20px;
  padding-bottom: 0px; 
  margin-bottom: 0px;
  font-size: 16px; 
  border: 0; 
  caret-color: #57be6a;
}
.uploader {
  margin-top: 20px;
  margin-left: 25px;
  
}
.list {
  width: 95%;
  margin: 0 auto;
  border-bottom: 2px solid #f2f2f2;
  zoom:1;
}
.list:after{
     display:block;
     content:'';
     clear:both;
     height:0;
     overflow:hidden;
}

.photo {
  width: 50px;
  height: 50px;
  background-color: #fff;
  margin-top: 10px;
  border-radius: 10px;
  overflow: hidden;
}
.photo img {
  width: 50px;
  height: 50px;
}
.name {
  width: 200px;
  height: 20px;
  margin-top: -45px;
  margin-left: 60px;
  color: rgb(73, 73, 173);
  font-size: 18px;
}
.text {
  width: 290px;
  margin-top: 25px;
  margin-left: 60px;
  font-size: 18px;
  overflow: hidden;
}
.pic {
  background-color: #fff;
  width: 260px;
  margin-top: 10px;
  margin-left: 55px;
  display: flex;
  flex-flow: wrap;
  
}

.pic img {
  width: 80px;
  height: 80px;
  margin-bottom: 5px;
  margin-left: 5px;
}
.more {
  width: 28px;
  height: 32px;
  background-color: #f7f7f7;
  float: right;
  margin-bottom: 10px;
  margin-right: 10px;
  border-radius: 5px;
  overflow: hidden;
}
.more img {
  width: 32px;
  height: 32px;
  margin-left: 4px;
}
.like {
  width: 170px;
  height: 40px;
  float: right;
  margin-top: -3px;
  margin-right: 5px;
  background-color: #4d5153;
  border-radius: 10px;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  color: #fff;
  text-align: center;
  line-height: 40px;
  font-size: 14px;
  animation: move 0.5s ease 0s;
}
/* 声明动画 关键帧 @keyframes 动画名称{} */
@keyframes move {
  from {
    right: 0px;
  }
  to {
    right: 45px;
  }
}

.like div {
  display: flex;
  align-items: center;
}
</style>
