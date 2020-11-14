<template>
  <div class="topPlayNav">
      <div class="back" @click="backClick"><img src="~assets/img/back.png" alt=""></div>
  </div>
</template>

<script>
export default {
    name:"TopPlayNav",
    methods: {
        backClick(){
            this.$router.go(-1)
        }
    },
}
</script>

<style scoped>
    .topPlayNav{
        height: 12.5vw;
        width: 100%;
        background-color: rgba(229, 71, 59);
        display: flex;
        align-items: center;
    }

</style>