<template>
<div class="mine-top">
  <div class="head-icon"><img src="~assets/img/yu.jpg" alt=""></div>
  <div class="head-name">
    <h4>GOD灬宇丶</h4>
    <img src="~assets/lv7.png" alt="">


  </div>
 </div>
 
</template>

<script>
 export default {
   name:'Minetop' ,
   components: {

   },
   data () {
     return {

     }
   },
 }
</script>

<style scoped>
.mine-top {
  height: 100px;
  background-color: rgb(245, 246, 247);
}
.head-icon {
  overflow: hidden;
  float: left;
  width: 50px;
  height: 50px;
  margin: 25px 20px 25px 30px;
  border-radius: 25px;
}
.head-icon img{
  width: 50px;
  height: 50px;

}
.head-name {
  float: left;
  position: relative;
  width: 200px;
  height: 50px;
  margin-top: 25px;
}
.head-name h4{
  position: absolute;
  top: -15px;

}
.head-name img {
 position: absolute;
 width: 24px;
 height: 24px;
 top: 20px;
 left: 40px;
}
 
</style>
